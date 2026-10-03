---
title: Task7 自测题知识点总结
url: https://www.yuque.com/ehsuh/oguki0/tqzdgx18083nqmu8
doc_id: 248112485
exported_at: 2026-10-03T22:20:26
---

配套《学习笔记-Task7-接口文档.md》使用 用法：每题先看「你的答案」对账，再看「参考答案」；**⚠️**** 标记的就是本轮答偏/答漏的地方**，那是重点 日期：2026-09-28 ｜ 项目：`C:\Users\ASUS\IdeaProjects\demo`

---

## 成绩单（2026-09-28 实测）
| 题 | 判定 | 关键词 |
| --- | --- | --- |
| Q1 | ✅ 满分 | 三方分工说清 + "先看注解再看 JSON"；小漏：没写网址 |
| Q2 | ⚠️ 半对 | 追到"版本不兼容"就停了；关键字空、修法空；**第 4 问答对** |
| Q3 | ✅ 满分 | `@Target` 判据 + `value` 省略规则，两条全对 |
| Q4 | ⚠️ 半对 | 位置判对；"大概 IDEA 允许的"**错**；正确写法空 |
| Q5 | ✅ 满分 | 显示名 vs 标识名分得很清；第 4 问概括空、第 2 问一个理由说偏 |
| Q6 | ⚠️ 半对 | `**helloPost**`** 的来源搞错了**（你以为是拼的，它就是方法名） |
| Q7 | ✅ 满分 | 全对 —— 含**我答错过两次**的第 3 问 |
| Q8 | ⚠️ 半对 | 第 1 问**理解反了**（是让你关，不是让你开） |
| ★附加 | ✅ 方向对 | "兜底太宽"点到了 |


**满分 4 / 半对 4 / 未答 0。**

有个细节值得你自己看一眼：**Q3 第 1 问你答对了"**`**@Target**`** 决定能不能贴"，Q4 第 2 问同一原理却答成"大概是 IDEA 允许的"** —— 不是不会，是**没往那道题上搬**。这一条比分数重要。

---

## Q1 · 文档的"真身"
### 参考答案
**1. 同一个东西，网址是 **`**http://localhost:8080/v3/api-docs**`**。**

⚠️ 你答对了"数据都来自 springdoc 包装成的 JSON"，但**没写出网址**。这个网址要记住，因为它是排查问题的唯一硬证据。

**2. 三方分工（你答得很完整）：**

| 角色 | 干什么 |
| --- | --- |
| 你的代码 | 提供全部内容（接口、字段、注解） |
| springdoc | 扫描代码 → **生成**`/v3/api-docs` 的 JSON |
| Knife4j / Swagger UI | 把 JSON **画成**网页（还内置免下载的调试功能） |


**3. "先看注解、再看 JSON"—— 完全正确。**

判"没生效"还是"只是没显示"，顺序是：

```plain
先看 /v3/api-docs 的 JSON 里有没有这段
  ├─ 有  → 注解生效了，是界面没展示（比如 Knife4j 不显示 tag 的 description）
  └─ 没有 → 注解真没生效 → 回去查：包选错了？没重启？贴错位置了？
```

**你原话"有的描述就是不会显示出来，但是 springdoc 打包的 json 里有"—— 这句话就是这一节的精髓。**

### 术语收紧
**"注解成员" → 标准叫法是「注解属性」（attribute）。**

`@interface` 里写 `String value();` 长得像方法，其实是**属性的声明**。这跟 Task6 那条"注解属性 ≠ 方法形参"是同一条线，**这已经是第二次磨这个词了**，记住就行。

→ 回看 第二、四节

---

## Q2 · 那个版本坑
### 你的答案
"这个我不知道，我只记得搞好 pom 依赖的时候我去找小i了，他说这里有个伪成功的坑，主要是版本不兼容导致的……它的报错貌似是被我们写的 globalexceptionhandler 接住了。"

**第 4 问是这题的精华，你答对了。** 前 3 问追到"版本不兼容"就停了。

### 参考答案
**1. 报错关键字（要能报出来）：**

```plain
java.lang.NoSuchMethodError:
'void org.springframework.web.method.ControllerAdviceBean.<init>(java.lang.Object)'
```

| 要素 | 内容 |
| --- | --- |
| 异常类型 | `NoSuchMethodError`（注意：是 **Error** 不是 Exception） |
| 缺失的东西 | `ControllerAdviceBean` 的**单参构造器** |


**2. 必然的版本问题，不是偶发。** 理由：

| 事实 | 说明 |
| --- | --- |
| Knife4j 4.5.0 发布于 2024-01，**之后再没发版** | 它内部拖的是 **springdoc 2.3.0**（老） |
| 你的项目是 **Spring Boot 3.5.16**（Spring Framework 6.2） | 新 |
| Spring 6.2 **删掉了**`ControllerAdviceBean` 那个构造器 | → 老 springdoc 调不到 → 崩 |


⇒ 只要"Spring Boot 3.4+ 配 Knife4j 4.5.0"，**必然踩**，跟你机器环境无关。

**3. 修法（pom 里动两处）：**

```plain
<exclusions>
    <exclusion>
        <groupId>org.springdoc</groupId>
        <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    </exclusion>
</exclusions>

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.15</version>
</dependency>
```

复验：`mvn dependency:tree -Dincludes=org.springdoc` → 全链路应为 2.8.15、**无 2.3.0 残留**。

**4. ****✅**** 为什么"能启动"会骗人（你答对了）：**

```plain
springdoc 初始化阶段抛 NoSuchMethodError
   ↓ 它是 Exception 的子类
被 Task6 的 @ExceptionHandler(Exception.class) 接住
   ↓
你看到的是 {"code":500,"message":"系统繁忙"} —— 而不是启动失败
```

**一句话**：**"进程活着" ≠ "功能正常"。** 判断依赖通不通，只看功能输出（JSON 有没有内容）。

### ⚠️ 本轮要补的
不是理解问题，是**没把硬信息记下来**：异常类型、缺的那个构造器名、pom 里动哪两处。这三个是**下次遇到同类问题的抓手**，值得背。

→ 回看 第三节

---

## Q3 · `@Info` 为什么不能平级写
### 参考答案
**1 & 2. 不能平级，原因是语法层面：**`**@Info**`** 的 **`**@Target**`** 只有 **`**ANNOTATION_TYPE**`**。**

```plain
@Target 声明一个注解"允许贴在哪"
ANNOTATION_TYPE 的含义 = 只能当"别的注解的属性值"存在
```

⇒ **编译器直接禁止**`@Info` 贴到类上。不是约定、不是 springdoc 的规矩，是**语言规则**。

```plain
@OpenAPIDefinition(info = @Info(title = "..."))   // ✅ 唯一正确写法
@Info(title = "...")                              // ❌ 编译不过
```

你答的"`@OpenAPIDefinition` 的注解属性是 `@Info`"——**对**，只是"不能平级"这半句你在第 1 问里顺带说了、第 2 问没再明确回答。

**3. ****✅**** 判据（你答对了）：**

**看它的 **`**@Target**`** 能不能独立贴在别处。** 能贴 FIELD/METHOD/TYPE → 独立注解（如 `@Schema`） 只有 ANNOTATION_TYPE → 只能当属性值 → 真·成员（如 `@Info`）

**4. ****✅**** **`**value**`** 省略规则（完全正确）：**

| 注解 | 有 `value` 吗 | 能省 `value = ` 吗 |
| --- | --- | --- |
| `@GetMapping` / `@RequestMapping` | 有 | ✅ `@GetMapping("/list")` |
| `@NotBlank` | **没有** | ❌ `@NotBlank("...")` 爆红 |
| `@OpenAPIDefinition` | **没有** | ❌ `@OpenAPIDefinition(info)` 爆红 |


**一条规则通吃**：括号里想省属性名，那个注解必须有一个叫 `value` 的属性。 你这次是**自己推出来的**，跟 Task6 被编译器打脸那次已经完全不是一回事了。

### 术语收紧
再说一次：叫**「注解属性」**，不是"注解成员"。判断父子关系也别用"成员"这个词，容易和 Java 类的成员变量混。

→ 回看 第六节

---

## Q4 · "编译能过 ≠ 用法正确"
### 你的答案
"不对，因为 tag 是修饰 controller 类的注解，我不知道他为什么能编译通过，大概是 idea 允许的🤔"

**第 1 问对，第 2 问答错（关键），第 3、4 问空。**

### 参考答案
**1. ****✅**** 位置不对。**`@Tag` 的语义是"给**一组接口**分组"，读者是 springdoc 的接口扫描器 —— **它只处理带 **`**@RestController**`** 的类**。`Result` 不是控制器，所以这个 tag 没有接口可归。

**2. ****⚠️**** 不是 IDEA 允许的，是 **`**@Tag**`** 自己的 **`**@Target**`** 含 **`**TYPE**`**。**

```plain
@Tag 的 @Target = [METHOD, TYPE, ANNOTATION_TYPE]
                          ↑ 有它，所以贴类上编译能过
```

`**@Target**`** 只负责"能不能编译"，一个字的语义都不管。** 这就是"编译能过 ≠ 用法正确"的机制。

⚠️ **这题的第一反应很关键**：你在 Q3 第 3 问刚答对"看 `@Target` 能不能独立贴"。Q4 第 2 问就是同一件事 —— **一个注解能贴在哪，只看它的 **`**@Target**`**，跟 IDE 没有半点关系**（IDEA 只负责高亮提示，编译器才是裁判）。 **同一个原理，两道题，一次对一次没对** —— 复习时先看这条。

**3. 语义对不对，由「读这个注解的程序」决定。**

这就是 Task6 那句「**注解谁读它**」的延续：

| 注解 | 读者 | 结果 |
| --- | --- | --- |
| `@TableName` | MyBatis-Plus | 类 ↔ 表映射 |
| `@NotBlank` | Hibernate Validator | 参数校验 |
| `@JsonProperty` | Jackson | JSON 序列化 |
| `@Tag` / `@Operation` / `@Schema` / `@OpenAPIDefinition` | springdoc | 文档 |


`@Tag` 贴到 `Result` 上，springdoc **不读它** → 写了等于没写（还可能多出个空分组）。

**4. 正确写法：类级 **`**@Schema(description = "...")**`**。**

```plain
@Schema(description = "统一返回结果")   // ✅
public class Result<T> { ... }
```

理由：`@Schema` 的 `@Target` 含 `TYPE`，而它的语义**就是**"描述这个数据模型"——贴类上是它的**正经用法**。

**同一个 **`**@Target**`** 含 TYPE 的两个注解（**`**@Tag**`** / **`**@Schema**`**），一个贴类上对、一个贴类上错** —— 差在**读者要不要它**。`@Target` 管编译，语义管对错，**两件事分开看**。

→ 回看 第七、八节

---

## Q5 · 名字的两种身份
### 参考答案
**1. ****✅**** springdoc 起的（你答对了）。**

`Result<T>` 一个泛型类 → 每个**具体泛型实例**都要有独立的 schema 名：

| 代码里的类型 | 生成的 schema 名 |
| --- | --- |
| `Result<User>` | `ResultUser` |
| `Result<List<User>>` | `ResultListUser` |
| `Result<Long>` | `ResultLong` |


你说的"因为 T 有三种使用可能"——就是这个意思，**说对了**。

**2. 两个理由（你对了 1 个、说偏 1 个）：**

| # | 理由 | 你的答案 |
| --- | --- | --- |
| ① | 它要当 `$ref` 的 **URI 片段**（`#/components/schemas/ResultUser`），URI 里 `<``>` 非法 | ✅ 答对了（"`<>` 很多地方不合规"） |
| ② | 它要被**代码生成器**拿去当类名（生成前端 TS 类型 / Java 客户端 SDK），`Result<User>` 不是合法标识符 | ⚠️ 你答的是"字符串里显示 `<>` 不美观" —— **不美观是表象，真正原因是"它要当类名"** |


记牢第 ② 条：**这不是美不美观的问题，是"这个名字要变成别的语言里的一个类名"**。

**3. ****✅**** 能写 **`**<>**`**，你的判断完全正确。**

`@Tag(name = "用户管理 <>")` 是**显示名**（给人看的标签），不受约束；`ResultUser` 是**标识名**（给机器用的 ID），受约束。

字符集你记了一半 —— 补全：

| | 允许的字符 |
| --- | --- |
| **标识名**（OpenAPI components 键名） | 字母、数字、`.`、`-`、`_` |
| **显示名** | 随便（中文、`<>`、emoji 都行） |


你记得 `.` 和 `_`，**漏了连字符 **`**-**`（`Result-Long` 这种也是合法的）。

**4. 你没答，补上这**一句话**：**

**工具推导出来的「标识名」受约束；自己写的「显示名」不受约束。**

→ 回看 第九节

---

## Q6 · `helloPost` 是什么
### 你的答案
"helloPost 是 hellocontroller 控制器下的方法，叫 hello，但他被 @postmapping 标记了，所以呈现的是 helloPost"

### ⚠️ 这里搞错了，是本题唯一的硬错误
`**helloPost**`** 不是"**`**hello**`** + **`**Post**`** 拼出来的"，它本身就是那个方法的名字。**

回看源码：

```plain
@PostMapping("/hello")
public String helloPost(){        // ← 方法名就叫 helloPost，一个字母都没拼
    return "PostMapping is running!";
}
```

`@PostMapping("/hello")` 只决定**路径**，方法名跟路径没有任何推导关系 —— `hello()` 和 `helloPost()` 是两个不同方法，`@GetMapping` 和 `@PostMapping` 各贴一个。

所以链路是：

```plain
方法名 helloPost
    ↓ springdoc 把它当 operationId
左侧菜单没有 summary 时用它兜底 → 显示 helloPost
```

**你答的"hello+Post"其实更接近"**`**POST /hello**`**"那个 Swagger UI 的显示规则**（方法+路径），两个界面串了。

### 参考答案
**1. 它是 **`**HelloController**`** 里的方法名**，被 springdoc 拿去当 `operationId` 了。不是路径、不是拼的。

**2. 两个界面在没写说明时的兜底规则（你没答）：**

| | 没 `summary` 时显示什么 | 加了 `@Operation(summary)` 之后 |
| --- | --- | --- |
| **Knife4j 左侧菜单** | `**operationId**`** 兜底** → `helloPost` | 变你写的中文（`你好，post`） |
| **Swagger UI** | **永远「HTTP 方法 + 路径」** → `POST /hello` | 还是「方法 + 路径」，**不跟着变** |


⇒ **Swagger UI 的列表从来不看 summary，它只认方法和路径。** 这是两个界面最容易串的地方。

**3. **`**@Operation**`** 的 **`**summary**`** 属性**（你答"用 operation"方向对，但要说准是哪个属性）。

```plain
@Operation(summary = "你好，post")   // ← 关键是 summary
```

顺带：`description` 属性**不进左侧菜单**，它只出现在右侧详情页里。

→ 回看 第十节

---

## Q7 · password 的两条防线 ⭐ 本轮最漂亮的一题
### 你的答案
"a 是写在 user 类的 password 属性上的 `@jsonproperty` 注解，属性是 WRITE_ONLY" "b 应该是 springdoc，**我应该没有多写注释，是 springdoc 读到我写的注释帮我写的**" "应该成立吧，因为我就写了这个" "进的是给 add、update 用的"

**四问全对。** 尤其第 3 问 —— 那是**我在这道题上错过两次的地方**。

### 参考答案
| 要防的 | 谁在管 | 手段 |
| --- | --- | --- |
| **A：响应里不出现 password** | **Jackson** | `@JsonProperty(access = WRITE_ONLY)`（Task6 已做） |
| **B：文档里标 **`**writeOnly**` | **springdoc** | **自动读 Jackson 的那个注解翻译过来** |


**3. ★ 只保留 **`**@JsonProperty(access = WRITE_ONLY)**`**，A 和 B 都成立 —— 你说的对。**

`/v3/api-docs` 里它就是：

```plain
"password": { "type": "string", "minLength": 1,
              "pattern": "[_a-zA-Z0-9]{6,20}", "writeOnly": true }
```

**没写任何 **`**@Schema**`**，**`**writeOnly: true**`** 自己就出来了。** 顺带 `@NotBlank` / `@Pattern` 也被自动翻成了 `required` / `minLength` / `pattern`。

**4. ****✅**** "只许进"的那一半 = **`**/user/add**`** 和 **`**/user/update**`**。**

| 接口 | 方向 | password 有用吗 |
| --- | --- | --- |
| `/user/add` POST | **进来**（反序列化） | ✅ 要读它来存库 |
| `/user/update` PUT | **进来** | ✅ 改密码要读 |
| `/user/list` GET | **出去**（序列化） | ❌ 被 `WRITE_ONLY` 挡掉 |


### ★ 这一题为什么值得单独说
我在这个点上**错过两次**：

| 我说过的 | 真相 | 我的病根 |
| --- | --- | --- |
| "`@JsonProperty(WRITE_ONLY)` 只管 Jackson，文档里照样显示 password，得加 `@Schema`" | **错**。springdoc 2.8.15 会自动翻 | 结论来自**还残留 springdoc 2.3.0 的临时副本**（那个副本里 springdoc 根本没初始化成功）—— **在坏了的环境里得出的观察不是观察，是噪音** |


**而你的判断只有一句："因为我就写了这个。"**

```plain
我：跨版本沿用旧结论  →  错
你：看"我到底写了什么"  →  对
```

**这题你赢在方法上**：**不知道该信谁的时候，先看"现场有什么证据"，不要信印象。** 这正是笔记里反复讲的那条规矩。  
反过来说，**我错得也不冤** —— 我该做的是重测，而不是把旧副本里的观察搬过来。

→ 回看 第十一节

---

## Q8 · 生产环境的那两条 WARN
### 你的答案
"他提醒我没有连上 springdoc.api-docs，**让我打开**"  
"大概是布尔开关吧"  
"生产环境小知讲过，但是我没注意😵"

### ⚠️ 第 1 问理解反了（笔记里专门警示过这一点）
**WARN 不是在提醒你"没连上"，也不是让你"打开"——它是在提醒你"这个端点是默认开着的，上线前记得关"。**

原文再读一遍：

```plain
SpringDoc /v3/api-docs endpoint is enabled by default.
  To disable it in production, set the property 'springdoc.api-docs.enabled=false'
                          ↑ disable（关闭）
```

`**enabled by default**`** = 默认已开启**（所以不用你做任何事就生效了）；`**To disable it in production**`** = 生产环境要关掉**。

### 参考答案
**1. 在提醒你：端点默认对所有人开放，生产环境必须关。** 是让你**关**，不是让你开。

**2. ****✅**** 布尔开关（你答对了）。** 读作"把 `api-docs` 端点设为不可用"：

| 配置 | 含义 |
| --- | --- |
| `enabled=true`（默认） | 端点**可用** → 任何能访问到的人都能拿到 |
| `enabled=false` | 端点**关闭** → 返回 404 |


它不是路径（不是"文档放在了 `/api-docs` 这个地址"那种意思）。

**3. 为什么生产必须关（你没答）——至少两条：**

| 风险 | 说明 |
| --- | --- |
| **接口清单全暴露** | 攻击者一眼看到你有哪些接口、要什么参数，等于送了一份地图 |
| **能直接发请求** | Knife4j 的调试功能是内置的 —— 没做鉴权的话，**改数据、删数据的接口都能点** |
| **内部信息外泄** | 字段名、数据结构、你写的注释全在 JSON 里 |


**4. 你现在的开发环境：不用改。**

理由：你**需要**它来写文档、调接口。**上线前再关**（可以用 `application-prod.properties` 单独配，这一点等真上线时再说）。

**一句话**：**开发开着，上线关掉** —— 别现在就去改，会把自己用的工具关没了。

→ 回看 第十三节

---

## ★ 附加思考题 · `favicon.ico` 的 404 变成 500
### 你的答案
"大概是我们写的 globalexceptionhandler 接的，可能是它默认我们有，没搜到就是故障了吧🤔，什么异常都能接的问题吧🤔，我觉得多加几个不同 exception 类型的方法"

**方向全对：谁接住的 ****✅****、兜底太宽 ****✅****、改法方向 ****✅****。** 补精确机制。

### 参考答案
**1. 谁接住的、怎么变成 500：**

```plain
浏览器自动请求 /favicon.ico
   ↓ 项目里没这个静态资源
Spring 抛 NoResourceFoundException（本该 → 404）
   ↓ 它是个 Exception 的子类
@ExceptionHandler(Exception.class) 声明"我接所有 Exception" → 被选中
   ↓
返回 {"code":500,"message":"系统繁忙"} + 一条 ERROR 日志
```

**关键**：`NoResourceFoundException` 在异常继承树上**是 **`**Exception**`** 的后代**，所以兜底那句"我接所有 Exception"把它也圈进去了。**不是"默认我们有"，是"它声明接的范围太大"。**

**2. 暴露的设计问题：兜底范围太宽。**

| | 应该怎样 | 实际怎样 |
| --- | --- | --- |
| "客户端请求了不存在的东西" | **404**（客户端的问题） | 被当成 **500**（服务端故障） |
| 日志级别 | 不该报 ERROR | **ERROR**（运维会被叫起来） |


⇒ 把**正常情况当成故障**，污染日志、误报监控。

**3. 怎么改（你的方向对，机制在这里）：**

`@ExceptionHandler` 挑处理器是 **按异常类型找最贴近的那个**（Task6 Q3 那条：靠类型不靠顺序）。

所以**不需要"多加几个"，加一个就够**：

```plain
@ExceptionHandler(NoResourceFoundException.class)   // ← 比 Exception 更贴近
public Result<Void> handleNoResource(NoResourceFoundException e) {
    return Result.error(404, "资源不存在");         // 具体方法名按你的 Result 写法
}
```

加了它之后，`NoResourceFoundException` 会**优先匹配到这条**，走不到 `Exception` 那条。

**一句话**：`@ExceptionHandler` 是"**谁更贴近用谁**"，所以**越具体的类型越优先** —— 兜底那条永远排最后。

（这条留到 Task8 一起收拾，Task8 本来就要重构 `BusinessException`。）

→ 回看 第十四节

---

# 附 · 本轮答漏/答偏的点（复习先扫这张表）
| # | 你答的 | 正解 |
| --- | --- | --- |
| 1 | `helloPost` = `hello` + `Post` 拼出来的 | **方法名本身就是 **`**helloPost**`；`@PostMapping` 只决定路径 |
| 2 | 那两条 WARN 是"提醒我没连上、让我打开" | 是提醒"**默认已开启**，生产要**关掉**" |
| 3 | `@Tag` 能贴类上"大概是 IDEA 允许的" | 是 `**@Tag**`** 的 **`**@Target**`** 含 **`**TYPE**`（IDEA 只提示，编译器才是裁判） |
| 4 | `Result<User>` 不能当名字，因为"显示 `<>` 不美观" | 因为它要当 **URI 片段 + 代码生成器的类名** |
| 5 | 报错关键字 / 修法（Q2）答不出 | `NoSuchMethodError` + `ControllerAdviceBean.<init>(Object)`；pom 里排除 2.3.0、显式换 2.8.15 |
| 6 | 术语说"注解成员"（第二次） | **注解属性（attribute）** |


**第 1、2、3 条是"该记住的事实没记住"；第 5、6 条是"没背硬信息/术语"；只有第 3 条是原理没搬过去。** 都不是理解能力的问题。

---

# 附 · 一句话速记（10 条）
1. `**/v3/api-docs**`** 那坨 JSON 才是文档本身**；`doc.html` 只是它的一种画法 → 页面不对先看 JSON
2. **Knife4j 一个字的文档都不产生**，页面内容不对要改注解/依赖
3. **"进程活着" ≠ "功能正常"**：`NoSuchMethodError` 被兜底接住，会伪装成 500
4. **Spring Boot 3.4+ 配 Knife4j 4.5.0 必然踩坑**（老 springdoc 2.3.0 调不到 Spring 6.2 删掉的构造器）
5. `**@Target**`** 只管"能不能编译"，语义由"读它的程序"决定** → 编译能过 ≠ 用法正确
6. `**value**`** 省略规则**：注解里必须有个叫 `value` 的属性才能省 `value = `
7. **显示名随便写，标识名受约束**（字母、数字、`.`、`-`、`_`）→ 中文只加在**显示名**上
8. **Knife4j 左侧用 **`**operationId**`** 兜底，Swagger UI 永远显示「方法 + 路径」**
9. **springdoc 2.8.15 自动读 **`**@JsonProperty(WRITE_ONLY)**`** → **`**writeOnly: true**`，不用额外写 `@Schema`
10. **开发开着文档，上线前关**（`springdoc.api-docs.enabled=false`）

# 
