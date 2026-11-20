---
title: 第 1 节 · User 实体 与 GlobalExceptionHandler
url: https://www.yuque.com/ehsuh/pggizs/rxmgrsoyvxdgcveq
doc_id: 292024353
exported_at: 2026-11-20T09:59:26
---

## 第 1 节 · User 实体 与 GlobalExceptionHandler
### 1.1 `@JsonProperty(access = WRITE_ONLY)` 到底是"哪边的 write"
**核心结论：Jackson 的 read / write 和 IO 的 read / write 不是同一套命名，别看成一个东西。**

| | read 指什么 | write 指什么 | 描述的是什么 |
| --- | --- | --- | --- |
| **Java IO** | `read()` 从流里**取**数据 | `write()` 把数据**塞进**流 | **数据流动的方向**（相对程序） |
| **Jackson / JavaBeans** | **getter**（read method） | **setter**（write method） | **属性的两个访问方法** |


Jackson 沿用的是 JavaBeans 规范的老叫法：getter 叫 "property read method"，setter 叫 "property write method"。

【引用·Jackson 官方对 `Access.WRITE_ONLY` 的定义】

"the property may only be written (**set**) for deserialization, but will not be read (**get**) on serialization"

括号里就是 set / get —— 证明它说的就是"只留 setter，去掉 getter"。

**所以 **`**WRITE_ONLY**`** 直接读成「只有 setter」**：

+ 前端 POST 带 password → 调 setter 写进对象 → ✅ 能收（`@NotBlank` 也能校验）
+ 对象 → JSON 响应 → 要调 getter → ❌ 拿不到，字段消失

**为什么初学者会懵**：同一个技术圈，IO 用 read/write 表示"方向"，Jackson 用 read/write 表示"方法名"，两套坐标撞词了。不是理解力问题。

**对立项：**`**@JsonIgnore**` Jackson 官方语义是 read、write **两个方向都忽略**。所以 password 若换成它，前端传来的密码**连收都收不到** → `@NotBlank` 报"密码不能为空" → add 直接 400。 一句话记：`**WRITE_ONLY**`** 是"能进不能出"，**`**@JsonIgnore**`** 是"进出一齐封死"。**

### 1.2 createTime 是谁填的
**不是 SQL 语句"自带"，是列定义给了默认值。**

【实测·2026-11-14 `SHOW CREATE TABLE demo_db.user`】

```plain
`create_time` datetime DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间'
```

完整链路：

1. Java 代码里**从没** set 过 `createTime`（`addUser()` 里一行都没有）；
2. MyBatis-Plus 默认写入策略是 `NOT_NULL` → 值为 null 的字段**不进 SQL**； 实际执行的是 `INSERT INTO user (username, password) VALUES (?, ?)`，压根没提 create_time；
3. MySQL 发现没给这列 → 用 `DEFAULT CURRENT_TIMESTAMP` 自己填。

**副作用（真实见过）**：insert 完，内存里那个 `user` 对象的 `createTime` 仍是 `null`， 而 `add` 接口返回的正是这个内存对象 → 响应里 `"createTime": null`。 库里那行是有时间的，只是对象没被回填。

想要有值：① insert 后重查一次 ② 给字段加 `@TableField(fill = FieldFill.INSERT)` 配自动填充。

### 1.3 `private static final Logger log = LoggerFactory.getLogger(X.class)`
**不是"把异常日志赋值给 log"，是"向日志框架要一支署名 X 的记录器"。**

| 部分 | 作用 |
| --- | --- |
| `LoggerFactory.getLogger(...)` | 向日志框架要一个记录器（入口在 SLF4J 这层） |
| 传 `.class` | 只要**名字**，不是要那个编译后的文件 |
| `static` | 一个类一份，不随对象重复创建（跟静态属性同理） |
| `final` | 拿到就不换 |


**署名在哪看**：控制台每行日志末尾那段就是它。

```plain
2026-11-07T09:41:24.328+08:00 INFO 1304 --- [demo] [nio-8080-exec-1] c.e.demo.service.impl.UserServiceImpl : 缓存未命中…
                                                                  └────────── 这就是署名 ──────────┘
```

**一个精确化**：日志框架不是"按类过滤"（过滤是按级别做的），它是给每条日志**盖章**，格式化时把章打出来。所以是"署名"，不是"筛子"。

### 1.4 `e.getBindingResult().getFieldErrors().get(0).getDefaultMessage()`
**为什么这么绕：因为校验失败时错误不是一条，是一批。**

用户什么都没填就提交，username 和 password 会**同时**报错。

| 那段 | 拿到什么 |
| --- | --- |
| `getBindingResult()` | 装"这次校验全部结果"的容器 |
| `getFieldErrors()` | 只要**字段级**错误 |
| `.get(0)` | 取第一条 |
| `getDefaultMessage()` | 取注解里写的 `message` 文本 |


**框架为什么不直接给一条**：它不知道你要报第一条、全报、还是拼起来 —— **决定权留给你**。

**字段级 vs 类级**：

+ **字段级（FieldError）**：错在某个属性上，带字段名。`username` 为空属于这类。
+ **类级（ObjectError）**：错在整个对象上、不属于任何单字段。典型是**跨字段校验**（"两次密码必须一致"——算 password 还是 confirmPassword 都不合适）。
+ 本项目只用字段级，所以 `getFieldErrors().get(0)` 够用。

**小纠正**：`getDefaultMessage()`**不是异常的方法**，是列表元素 `FieldError` 的方法。

### 1.5 四种"看异常"的写法（易混，重点）
| 写法 | 输出什么 | 走哪条通道 | 进日志文件吗 |
| --- | --- | --- | --- |
| `e.getMessage()` | 只有消息文本（没写就是 null） | 返回给你，随你处置 | 看你怎么用 |
| `e.toString()` / `"" + e` / `sout(e)` | `类名: 消息`，**一行，无堆栈** | —— | —— |
| `log.error("x", e)` | 一行消息 + **完整堆栈** | 日志框架 | ✅ |
| `e.printStackTrace()` | 完整堆栈 | **System.err**，绕过日志框架 | ❌ |


**关键坑**：只有把 `e` 作为**最后一个参数**、且**前面没有对应的 **`**{}**`，SLF4J 才认得"要打堆栈"。

```plain
log.error("系统繁忙", e);      // ✅ 带堆栈
log.error("系统繁忙 {}", e);   // ❌ 退化成 toString，只有一行
log.error("系统繁忙", e.getMessage()); // ❌ 只有消息
```

`**printStackTrace()**`** 不是"违法"，是"该走大门的货走了后门"**：

1. 不经过日志框架 → 不受级别控制（你设成 WARN 它照样打）；
2. 不带时间戳 / 线程名 / 署名，也不进日志文件；
3. 生产环境 `System.err` 可能压根没被收集 → 你以为记了，其实什么都没留下。

**SLF4J 是什么**：一层"日志门面"。你的代码只调它，它转给底下的真实现（Logback / Log4j2）。 好处是代码不绑死某一家，换实现不用改业务代码。`LoggerFactory` 就是这层的入口。 （它不是 JVM 的功能，是一个普通的三方库。）

### 1.6 `getParameterName()` 用在哪
项目里就在 `handleMissingParam` 那一处：

```plain
@ExceptionHandler(MissingServletRequestParameterException.class)
public Result<Void> handleMissingParam(MissingServletRequestParameterException e){
    log.warn("缺少必需参数: {}", e.getParameterName());
    return Result.error(400, "缺少必需参数：" + e.getParameterName());
}
```

它**不打印任何东西**，只是返回一个字符串 —— `@RequestParam String q` 缺值时返回 `"q"`。 是**请求参数名**（你在 `@RequestParam` 后面写的那个变量名），不是实体属性名。

### 1.7 日志安全：判据不是"落不落盘"
**错判**：以为"只要日志不写到磁盘就没事"。

**判据有两层：内容是根本，流向是放大器。**

先说流向 —— 这条日志会不会离开你的控制范围。三条路都会离开：

1. 写进磁盘文件 → 被拷走、被备份带走；
2. 被采集 → 公司统一日志平台，权限更高的人都能搜；
3. **你贴给别人** → 群、工单、AI 对话 ← 这条最常见，本项目就发生过。

**但堆栈本身不敏感。** 敏感的是**业务数据**（密码、密钥、身份证、手机号），不是**代码位置**（类名/行号/方法名）。

所以"打全栈"和"别泄露密码"不矛盾 —— 它们管的是两类不同的东西：

| 去向 | 该给什么 | 本项目做法 |
| --- | --- | --- |
| 响应（用户/前端） | 模糊一句话 | `Result.error("系统繁忙，请稍后重试")` |
| 日志（你/运维） | 越详细越好 | `log.error("系统繁忙", e)` |


**什么时候反而不该打全栈**：高频、零信息量的预期异常。favicon 404 就是范例 —— 每次开网页都来一次，打全栈会刷屏。那是**噪音控制**，不是安全。

**堆栈怎么看**（三眼够用）：

1. 第一行 / 第一个 `Caused by:` → 是什么错
2. 往下找第一个 `com.example.demo` → 错在你哪一行
3. 最底下的 `Caused by` → 真根因

### 1.8 七个 handler 分工表
| Handler | 谁抛的 | 触发场景 | 用户看到 |
| --- | --- | --- | --- |
| `MethodArgumentNotValidException` | `@Valid @RequestBody` | **body 里字段**校验失败（username 空、password 格式错） | 400 + 注解里的 message |
| `MissingServletRequestParameterException` | `@RequestParam` | **URL 上参数缺失**（`/rag/search` 不带 q） | 400 + "缺少必需参数：q" |
| `BusinessException` | 我们自己 `throw` | id 不存在、用户名重复 | 404 / 409 + 自定义消息 |
| `NonTransientAiException` | Spring AI | **重试也没用**的错：key 无效、余额不足、模型不存在、请求参数不合法 | 503 |
| `ResourceAccessException` | Spring 的 HTTP 客户端 | **TCP 层面就没成功**：DNS 失败、连不上、读超时 | 503 |
| `NoResourceFoundException` | Spring MVC 静态资源 | favicon.ico 之类 404 | 404 |
| `Exception` | 兜底 | 以上都没接住 | 500 + "系统繁忙" |


**前两个不冲突**：一个管**请求体**里的字段，一个管**URL 上**的参数。谁抛取决于 Spring 在哪一步失败。

**三个名字要记准**：

+ `MissingServletRequestParameterException` = **缺少必需请求参数**，不是"URL 错了"（URL 错了是 404）。
+ `ResourceAccessException` = **资源访问异常**，指的是连接/超时层面失败；"请求不通过"（4xx）不属于它。
+ `NonTransientAiException` 里的"参数不合法"指 **API 请求本身格式错**（模型名拼错、temperature 越界）， **不是**用户问的内容被审核。内容审核是另一回事（平台返回 4xx + 特定 message）， 虽然也可能落到 NonTransient（因为重试没用），但两者在日志里长得不一样。

### 1.9 本节易混清单（复习先看这里）
1. **IO 的 read/write = 方向；Jackson 的 read/write = getter/setter。** 撞词，不同体系。
2. `**WRITE_ONLY**`** = 只有 setter = 能进不能出。** 不是"只写不读"这种含糊说法。
3. `**@JsonIgnore**`** 两向都封**，不能拿它代替 `WRITE_ONLY`。
4. **createTime 是数据库列的 **`**DEFAULT CURRENT_TIMESTAMP**`** 填的**，不是 SQL 魔法，也不是框架。
5. `**getLogger(X.class)**`** 是"署名"，不是"过滤"；**`**.class**`** 要的是名字，不是编译文件。**
6. `**getDefaultMessage()**`** 是 **`**FieldError**`** 的方法，不是异常的方法。**
7. `**log.error("x", e)**`** 才带堆栈**；加了 `{}` 或传 `getMessage()` 都退化成一行。
8. `**printStackTrace()**`** 的问题是走错通道，不是"泄露"。**
9. **日志安全看"流向"，不看"落不落盘"；敏感的是业务数据，不是堆栈。**

### 1.10 第二轮修正（复述后补的精确版）
**① 两套 read/write：方向是「反的」，不是「一样」**

| | 参照物 | read | write |
| --- | --- | --- | --- |
| **IO** | 程序 | **进**程序 | **出**程序 |
| **Jackson / JavaBeans** | 属性 | 从属性**出**（getter） | 往属性**进**（setter） |


不能笼统说"本质都是流入流出" —— **两边都讲方向，但参照物一换，方向正好对调。**

最实用的记法：`WRITE_ONLY` = **只有 setter** = **只进不出**。

**② NonTransient vs ResourceAccess：判据是「对方有没有收到」**

| 异常 | 谁出问题 | 典型场景 | 重试有意义吗 |
| --- | --- | --- | --- |
| `NonTransientAiException` | **对方收到了，明确拒绝** | key 无效(401)、余额不足(402)、模型不存在(404)、请求格式错(400) | ❌ 没用 |
| `ResourceAccessException` | **压根没连上 / 等太久** | DNS 失败、连接被拒、读超时 | ✅ 可以 |


一句话：**一个"被拒绝"，一个"没送到"。**

**③ 缺参数：路径错 ≠ 参数缺**

| 请求 | 结果 |
| --- | --- |
| `/rag/searh?q=x`（**路径**拼错） | 404 `NoResourceFoundException` |
| `/rag/search`（**不带** q） | 400 `MissingServletRequestParameterException` |
| `/rag/search?q=`（q 存在但为空串） | **不抛异常**，`q = ""` 一路进 service |
| `/rag/search?q=%20%20`（只有空格） | **不抛异常**，`q = " "` 进 service |


`@RequestParam` 的 `required` 默认是 `true`，但它只管"**参数在不在**"，不管"**值空不空**"。 本项目 `RagController` 的 `q` 就是这种情况 —— 空串会传到 service，需要在那边处理（可以改进）。

**④ 日志署名：只取决于「哪一行代码调用了 log」**

不是"出错的类没写日志，handler 代打"，而是 —— **handler 里那行 **`**log.warn(...)**`** 是 handler 自己写的**，所以署名是 handler。跟异常从哪来无关。

证据：如果 service 也写一行 `log.warn`，会出现**两条日志、两个署名**。

**该在哪打**：

| 类型 | 在哪打 | 理由 |
| --- | --- | --- |
| 业务异常（404/409，可预期） | 交给 handler 统一打就够 | 重复打没有新信息 |
| 技术异常（Redis 挂、SQL 错） | **在源头打** | 那里才有上下文（哪个 key、哪条 SQL） |


**⑤ 字段级错误：多条不同错误，不是同一条重复**

`username` 空 → 一条 `FieldError(field="username", msg="用户名不能为空")``password` 空 → **另一条**`FieldError(field="password", msg="密码不能为空")`

所以 `get(0)` 取的是"第一条"，不是"唯一那条"。

**⑥ **`**printStackTrace**`** 不是被淘汰，是「用错了场合」**

| 场合 | 能用吗 |
| --- | --- |
| `main` 里临时调试、小脚本、命令行工具 | ✅ 正常 |
| Web 服务 / 长期运行的服务端 | ❌ 不该用 |


另两处小修：

+ `System.out.println` 走 **System.out**；`printStackTrace()` 走 **System.err**，两个通道。
+ 它不是"放生"，**控制台有接收**，只是没人把它写进日志文件。

输出内容也不是"只有堆栈"：**第一行是 **`**类名: 消息**`**，后面才是 **`**at ...**`。

**⑦ 本项目就有一个「绕过日志框架」的现成例子**

```plain
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

`StdOutImpl` = **直接往 System.out 打**。所以所有 SQL 和参数，走的是同一个"野通道"。

学习项目无所谓，生产要改：

```plain
# 删掉 log-impl 那行，改成只对 mapper 包开级别控制
logging.level.com.example.demo.mapper=info
```

三个后果：不受级别控制 / 生产可能被重定向落盘 / **SQL 日志会打出真实参数值**（用户名、密码哈希）。

### 1.11 日志框架是什么：一条"生成流水线"，不是"仓库"
**常见误解**：以为"日志本来就都存在框架里，我们只是把其中一部分打出来"。

**不是。日志不是"存着的"，是"你写了才生成"。** 你不调 `log.info`，这条记录从头到尾不存在。

日志框架 = 一条流水线，四段：

| 段 | 部件 | 干什么 |
| --- | --- | --- |
| ① 入口 | **Logger** | 你调 `log.info(...)` 的地方，把这条消息投进去 |
| ② 门槛 | **Level** | 低于配置级别的直接丢弃（默认 INFO，所以 debug 不出现） |
| ③ 包装 | **Encoder / Layout** | 加上时间戳、级别、线程名、署名，拼成一行 |
| ④ 发货 | **Appender** | 决定发到哪：控制台 / 文件 / 网络 |


**"其余的都还在里面"这个想法要丢掉** —— 没有"其余"。

唯一的例外：**框架和第三方库自己也在调 log**（Spring 启动横幅、Hikari 连接池、MyBatis 的 SQL）。那些是"别人写进去的"，不是"系统自动记录的"。

### 1.12 Class 对象：JVM 给每个类做的"说明书"
**定义**：Class 对象 = JVM 加载一个类时，为它创建的一张**运行时说明书**，里面装着这个类的全部结构信息（类名、包名、父类、接口、字段、方法、构造器、注解）。

**四个必答点**：

| 问题 | 答案 |
| --- | --- |
| 谁创建 | **JVM**，在类加载时（不是 `new` 的时候） |
| 一个类几个 | **一个**，全局唯一 |
| 什么时候建 | 第一次用到这个类时（首次 `new` / 首次调静态方法 / `Class.forName`） |
| 构造器私有影响吗 | **不影响** —— 它描述的是"类"，不是"实例" |


**它解决什么问题**：Java 是"运行期才拼装"的语言，有些事编译期根本定不下来 —— Spring 要问"哪些类上有 `@RestController`"、Jackson 要问"这个类有哪些 getter"、MyBatis 要问"这个类有哪些字段"。 **这些都得在运行时回答，而 Class 对象是唯一入口。** 这套机制叫**反射**。

`**X.class**`** 这个语法**：把 X 的 Class 对象给我。不是属性、不是文件、不是方法调用。

**和 Spring Bean 的关系（容易混）**：

| | 谁创建 | 什么时候 | 是什么 |
| --- | --- | --- | --- |
| **Class 对象** | JVM | 类加载时，每类一次 | 类的**说明书** |
| **Bean** | Spring | 容器启动时，按配置 | 一个可用的**实例** |


方向对（都是"框架替你先造好"），但**层级不同**：Class 对象在 JVM 层，Bean 在 Spring 层。

**日志里那个名字**：`getName()` 返回的是**全限定名**`com.example.demo.exception.GlobalExceptionHandler`； 日志显示的 `c.e.demo.exception.GlobalExceptionHandler` 是 Logback 的**缩写格式**（中间包名取首字母），**缩写是显示层做的，不是名字本身**。

### 1.13 钉死 NonTransient / ResourceAccess（口诀版）
换个讲法，抓一个动作：**"收到了吗？"**

| 情形 | 打比方 | 异常 |
| --- | --- | --- |
| 打不通（关机、占线、没人接、说到一半断了） | 通信没成功 | `ResourceAccessException` |
| 打通了，对方说"你打错了 / 我不办这事" | 通信成功但被拒 | `NonTransientAiException` |


所以：

+ **NonTransient 的前提是"通信成功"** —— 对方收到了请求，并且回了一个明确的错误响应（4xx）。
+ **"我们没接到对方的回复" → 仍然是 ResourceAccess**，不是 NonTransient。

一句话：**没收到 = ResourceAccess；收到了但不行 = NonTransient。**

### 1.14 三处小补充
**① 什么时候扣 token**

| 情况 | 扣吗 |
| --- | --- |
| 请求没送达（DNS 失败、连不上） | ❌ 不扣，对方还没开始算 |
| 对方**生成完**、返回路上断了 | ✅ **照扣**，它已经算过了 |


所以"超时"的代价不只是没拿到货，还可能白花钱 —— 超时设短一点能减少损失。

**② 映射 ≠ 反射**

| 词 | 意思 | 例子 |
| --- | --- | --- |
| **映射**（mapping） | 结构**对应** | `create_time` ↔ `createTime` |
| **反射**（reflection） | 运行时**读类结构、按需取用** | Spring 扫注解、Jackson 找 getter |


Class 对象是"说明书"，反射是"翻说明书办事"这个动作。别把两者混成一个词。

**③ URL 结构与三类参数注解**

```plain
https://host:8080/user/list?q=abc&topK=5
└─┬─┘   └─┬─┘└┬┘└───┬──┘└────┬─────┘
 协议    主机  端口  路径    查询串
```

| URL 里的位置 | 对应注解 |
| --- | --- |
| 路径中的 `{}` 占位（`/delete/{id}`） | `@PathVariable` |
| 查询串（`?q=abc`） | `@RequestParam` |
| 请求体（POST 的 body） | `@RequestBody` |


**路由前缀**（`@RequestMapping("/user")`）是路径的一部分，不是独立成分。 所以"URL 拼错"通常指**路径段**错（→ 404），"没带参数"指**查询串缺项**（→ 400）。

