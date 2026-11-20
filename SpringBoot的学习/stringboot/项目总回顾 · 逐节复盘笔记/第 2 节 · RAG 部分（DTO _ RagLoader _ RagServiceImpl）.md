---
title: 第 2 节 · RAG 部分（DTO / RagLoader / RagServiceImpl）
url: https://www.yuque.com/ehsuh/pggizs/tc2yns6ft0sg9z2d
doc_id: 292100878
exported_at: 2026-11-20T09:59:28
---

### 2.1 DTO 解耦的到底是「谁」
**全称**：Data Transfer Object（数据传输对象）—— 他记成 datatransmitobject，意思对，拼写是 Transfer。

`RagHit` 夹在两个"会变的邻居"中间：

```plain
Spring AI 的 Document ──▶ RagHit ──▶ Controller / 前端
        ↑ 换向量库就变         ↑ 稳定的形状      ↑ 不想跟着变
```

所以"框架"指的是 **Spring AI 那一套（**`**Document**`** / **`**VectorStore**`**）**，不是千问 embedding。 千问 embedding 在更下层，它只吐 `float[]`，连 `Document` 都不是。

**解耦的收益**：哪天把 `SimpleVectorStore` 换成 Milvus / Redis Stack，只改 `search()` 里那段映射，Controller 和前端一行不动。

### 2.2 读文件：`new String(bytes, UTF_8)` 已经解过码了
```plain
String content = new String(r.getInputStream().readAllBytes(), StandardCharsets.UTF_8);
```

拆成三步看：

| 步骤 | 干了什么 |
| --- | --- |
| `r.getInputStream()` | 拿到**字节流**（一根水管） |
| `.readAllBytes()` | 一次抽干，得到 `byte[]` |
| `new String(bytes, UTF_8)` | **按 UTF-8 把字节数组解码成字符串** |


**关键：**`**new String(byte[], Charset)**`** 本身就是解码动作。** 字符流（`InputStreamReader`）内部做的也是这件事，只是它边读边解、适合大文件。

| 写法 | 谁解码 | 适合 |
| --- | --- | --- |
| `new String(bytes, UTF_8)` | `String` 构造器，一次性 | 小文件（我们 62 KB） |
| `InputStreamReader` + `BufferedReader` | 字符流内部，边读边解 | 大文件、要按行读 |


所以"Sring 自带解码器"这个猜测 **是对的** —— 构造器吃一个 `Charset`，内部就用对应的 `CharsetDecoder`。 本项目选一次性读完，是因为文件小、还要整体切块，边读边处理反而麻烦。

### 2.3 `byte` 和 `char`（ byte 记成 type 了）
| | 位数 | 范围 | 含义 | 属于 |
| --- | --- | --- | --- | --- |
| `**byte**` | 8 | −128 ~ 127 | **数值**（一个字节） | 字节流 |
| `**char**` | 16 | 0 ~ 65535 | **字符**（一个 UTF-16 单元） | 字符流 |


"读进来转成 byte 是不是多余"—— 不多余，`readAllBytes()` 返回的**就是**`byte[]`，只是当场被 `new String` 吃掉了，所以在代码里看不见中间那一步。

### 2.4 metadata 为什么是 `Map<String, Object>`
`doc.getMetadata()` 的类型是 `Map<String, Object>`。值写 `Object`，是因为**一张表要装多种类型**：

```plain
"source"      → String   （文件名）
"chunk_index" → Integer  （第几块）
"section"     → String   （所属二级标题）
```

**Map 只能有一个值类型**，于是取最宽的 `Object`。

由此带来两个后果：

1. `**get()**`** 的编译期类型是 Object** —— 哪怕里面装的是 `Integer`，编译器也只认 Object。

```plain
int idx = doc.getMetadata().get("chunk_index");   // ❌ 编译不过
```

必须显式转换。

1. **所以才有那两行**：

```plain
Object ci = doc.getMetadata().get("chunk_index");
int idx = (ci == null) ? 0 : Integer.parseInt(ci.toString());
```

`**get()**`** 返回的不是键值对，是值** —— 键值对是 Map 内部的结构，`get(key)` 给你的是那个 key 对应的 value。

**当前写法的两个可改进点**（不影响运行）：

| 写法 | 问题 | 更直接的做法 |
| --- | --- | --- |
| `Integer.parseInt(ci.toString())` | 转字符串再解析回数字，绕一圈 | `((Number) ci).intValue()` 或 `(int) ci` |
| `String.valueOf(doc.getMetadata().get("source"))` | 值为 null 时返回字符串 `"null"`，不是 null | 先取出来判空，再 `toString()` |


### 2.5 `String.lines()` 是什么
`sec.lines()` —— **Java 11+ 的方法**，把字符串按行切成一个 `Stream<String>`。

+ 识别三种换行：`\n`、`\r\n`、`\r`
+ 返回的是 **Stream**，不是数组
+ 配 `.findFirst().orElse("")` = 取第一行，取不到给空串

本项目用途：拿这一节的标题行。因为切块用的是 `(?m)^(?=## )`（零宽断言，保留分隔符），所以每节第一行正好是 `## xxx`。

### 2.6 异常怎么走到 handler
**不是"controller 解决不了再交给 handler"**，而是**沿调用栈往上抛**：

```plain
Service 里 throw
   ↓ 栈展开（中间层的 finally 会执行）
Controller 方法当场中断，异常继续往上
   ↓
DispatcherServlet 捕获
   ↓
找 @RestControllerAdvice 里匹配的 @ExceptionHandler
   ↓
执行 handler 方法 → 返回值被写成 HTTP 响应
```

两点确认：

+ **"抛出点之后的代码不执行"** ✅ 对，这叫栈展开；
+ **handler 不在 controller 里跑**，它是 Spring MVC 在异常穿出 controller **之后**接手的。

### 2.7 流、单位、容器：三个不同的东西
这三个概念经常被搅在一起，分开就清楚了：

| 层 | 是什么 | 有哪些 | 举个例子 |
| --- | --- | --- | --- |
| **流** | 搬运的**通道/方式** | `InputStream` / `Reader` | `r.getInputStream()` 返回的那个对象 |
| **单位** | 搬运时**最小计量的东西** | `byte`（8 位）/ `char`（16 位） | `read()` 一次给你一个单位 |
| **容器** | 搬完之后**装在哪** | `byte[]` / `char[]` / `String` | `readAllBytes()` 返回 `byte[]` |


**对应关系**：

| 流 | 单位 | 一次读一个 | 一次读全部 |
| --- | --- | --- | --- |
| `InputStream` | `byte` | `read()` → `int`（0~255） | `readAllBytes()` → `byte[]` |
| `Reader` | `char` | `read()` → `int`（0~65535） | 需自己传 `char[]` 缓冲区 |


**关键纠正：**`**char**`** 没有解码器。**

+ **解码器在 **`**InputStreamReader**`** 里**，不在 `char` 里；
+ `char` 是**解码之后的结果**，不是解码工具；
+ 所以"用 char 保存会拆出乱码"这个担心不成立 —— **乱码发生在解码那一刻**（编码表用错），不在 char。

`String` 也不是"带解码器的容器"，而是"不可变的字符序列"，它的构造器**接受**一个 `Charset` 去调用解码器。工具在构造器调用的 `CharsetDecoder` 那儿。

`**getInputStream()**`** 时一个字节都还没读** —— 它只是"打开了一根水管"。真正读是 `readAllBytes()` 那一刻。所以不存在"把文件转成 byte"这个动作：**文件里本来就是字节，读出来就是字节。**

#### 2.7.1 为什么 3 个字节的汉字，不会撑爆 16 位的 char
这是他最容易绕进去的一处。答案一句话：

**解码是"查表翻译"，不是"把字节往 char 里塞"。**

```plain
UTF-8 的 3 个字节 (E4 B8 AD，共 24 位)
        ↓ 解码器查表
   码点 20013（十进制的"中"）
        ↓ 存进去
   1 个 char（16 位，最大 65535）→ 20013 装得下 ✅
```

**字节数与 char 个数没有换算关系**：

| 字符 | UTF-8 占字节 | 解码后占 char | 为什么 |
| --- | --- | --- | --- |
| `A` | 1 | 1 | 码点 65 |
| `中` | 3 | 1 | 码点 20013，< 65535 |
| `😀` | 4 | **2** | 码点 128512，**> 65535** → 拆成代理对 |


**所以“超范围”确实存在，但发生的条件是「码点 > 65535」，不是「字节数 > 2」。**

`byte` 永远不会因为“字符太大”而丢数据 —— 它只装 0~255，一个字节就是一个字节。丢数据只可能发生在 `char` 这一层，且只在 emoji 这类字符上。

**最容易混的一点：字节 ≠ 码点。**

| 阶段 | 是什么 |
| --- | --- |
| 字符 `中` | 语言里的那个字 |
| 码点 **20013** | Unicode 发给它的**编号** |
| `E4 B8 AD` | 按 UTF-8 规则把编号**写成**的 3 个字节 |


+ **编码（encode）** = 编号 → 字节，发生在**写文件**时；
+ **解码（decode）** = 字节 → 编号，发生在**读文件**时。

我们 `new String(bytes, UTF_8)` 走的是**解码**，不是编码。

`char` 里装的是 **20013 这个数字**，不是那三个字节。

#### 2.7.2 用字符流怎么写（对照版）
```plain
// 写法一：字符流按行读（Java 8 及以前的标准姿势）
try (BufferedReader br = new BufferedReader(
        new InputStreamReader(r.getInputStream(), StandardCharsets.UTF_8))) {
    StringBuilder sb = new StringBuilder();
    String line;
    while ((line = br.readLine()) != null) {
        sb.append(line).append("\n");
    }
    String content = sb.toString();
}
```

```plain
// 写法二：自己给 char[] 缓冲区（更底层，能控制每次读多少）
try (Reader reader = new InputStreamReader(r.getInputStream(), StandardCharsets.UTF_8)) {
    char[] buf = new char[8192];
    int n;
    StringBuilder sb = new StringBuilder();
    while ((n = reader.read(buf)) != -1) {   // 一次读 8192 个字符
        sb.append(buf, 0, n);                // 只取实际读到的 n 个
    }
    String content = sb.toString();
}

```

```plain
// 写法三：Files（Java 11+，一行顶上面那一坨）
String content = Files.readString(Path.of("a.md"), StandardCharsets.UTF_8);
```

**三者结果一样**：都得到 `String`。区别只在“谁来管缓冲、谁能边读边处理”。

我们项目用的 `new String(readAllBytes(), UTF_8)` 是**写法三的思路**（一次性），只是入口从 `Files` 换成了 `Resource`。

### 2.8 Stream 是惰性的：不调「终止操作」就一行都不会跑
Stream 的操作分两类：

| 类型 | 有哪些 | 行为 |
| --- | --- | --- |
| **中间操作** | `map` / `filter` / `sorted` / `distinct` / `limit` | 返回**新的 Stream**，**不执行** |
| **终止操作** | `collect` / `findFirst` / `forEach` / `count` / `toList` / `anyMatch` | **触发执行**，返回结果 |


所以：

```plain
sec.lines().findFirst().orElse("")     // ✅ findFirst 是终止操作，会执行
sec.lines().map(String::trim)          // ❌ 没有终止操作，一行都不跑
```

`findFirst()`**不是"内部调用了 collect"**，它本身就是终止操作，和 `collect` 平级。

**什么时候该用 Stream**（他问的"不知道什么时候用"）：

| 场景 | 用什么 |
| --- | --- |
| 数据**从 A 形态变成 B 形态**（过滤、转换、汇总） | Stream |
| 对每个元素**做一件事**（打印、写库、调接口） | `for` 循环更清楚 |
| 循环里有复杂控制流（多层 `break` / `continue`、改外部变量） | `for` 循环 |


一句话判据：**"我要一个结果"→ Stream；"我要做一件事"→ for。**

#### 2.7.3 码点超过 65535 时，是怎么“切”的（代理对）
**不是“取最大值 + 剩下的数”**，而是**拆成两个 10 位**，各自加一个固定偏移。

算法（UTF-16 规定）：

```plain
码点 - 0x10000  →  得到一个 20 位的数
  高 10 位 + 0xD800  →  高位代理（0xD800 ~ 0xDBFF）
  低 10 位 + 0xDC00  →  低位代理（0xDC00 ~ 0xDFFF）
```

拿 `😀`（U+1F600，十进制 128512）实算一遍，正好对上之前的实测值：

```plain
0x1F600 - 0x10000 = 0xF600
0xF600 的 20 位：0000 1111 0110 0000 0000
  高 10 位 = 0000111101 = 0x03D  →  +0xD800 = 0xD83D = 55357  ✅
  低 10 位 = 1000000000 = 0x200  →  +0xDC00 = 0xDE00 = 56832  ✅
```

这就是 `charAt(1)=0xD83D`、`charAt(2)=0xDE00` 的来源。

**所以“切”不是随便切，是查表算出来的两段。**

#### 2.7.4 String 不只是 char 数组
**概念上**：String 是一串字符。 **实现上（Java 9+）**：内部是 `byte[]` + 一个 `coder` 标记（Latin-1 或 UTF-16），叫 **Compact Strings**（紧凑字符串）—— 纯英文只占 1 字节/字符，省一半内存。

**它确实能分辨“哪几个 char 是同一个字”**，但方式不是自动合并，而是**提供按码点操作的 API**：

| 方法 | 对 `"A😀中"` 返回 |
| --- | --- |
| `length()` | **4**（char 数，emoji 算 2） |
| `codePointCount(0, length())` | **3**（真字符数） |
| `codePointAt(1)` | **128512**（emoji 真码点） |


`**char**`** 没有这个能力** —— 单个 char 没法表达“我和下一个是一对”。所以凡是要“按真正的字”处理，就得用 `codePoint*` 系列方法，不能用 `charAt`。

#### 2.7.5 `char` 打印时，Unicode 表在哪
**不在 char 里，在显示端。**

`char` 里就一个数字 20013。`System.out.println('中')` 把这个数字交给控制台，**控制台/字体**去查表找字形画出来。

所以“char 内部有表”是误解 —— 数据端只有编号，渲染才需要表。

#### 2.7.6 怎么判断“这两个 char 是一个字”
**靠取值范围，不靠“数位”。**

Unicode 把 `0xD800 ~ 0xDFFF` 这 2048 个值**专门保留**给代理对，**正常字符永远不用它们**。所以：

| 值落在 | 含义 |
| --- | --- |
| `0xD800 ~ 0xDBFF` | 高位代理（一个字的前半） |
| `0xDC00 ~ 0xDFFF` | 低位代理（一个字的后半） |
| 其他 | 独立的字 |


判断规则：**看到高位代理，再看下一个是不是低位代理**；两个都对上 = 一个字符。

**为什么不会误判**：因为这段区间被“预留”了，正常字符不会落到这里。这不是“猜”，是“查号段”。

**一个附带结论**：char 能装的范围**不是**`0~0xFFFF` 全部，而是 `0~0xD7FF` 和 `0xE000~0xFFFF` 两段，中间那 2048 个值被征用了。

**BMP**（Basic Multilingual Plane，基本多语言平面）= `U+0000 ~ U+FFFF`，一个 char 装得下，涵盖绝大多数常用字符（拉丁字母、汉字、假名、韩文）。Unicode 一共 17 个这样的平面，BMP 是第 0 个。

---

### 2.9 Unicode 与编码体系 · 汇总（第 2 节的收口）
#### ① 一个字符的"一生"
```plain
字符 '中'
  ├─ Unicode 发编号  →  码点 20013（U+4E2D）        ← 身份，永不变
  ├─ UTF-8 编码      →  3 字节 E4 B8 AD             ← 存文件时用
  ├─ UTF-16 编码     →  1 个 char（0x4E2D）          ← Java 内存里用
  └─ 显示            →  控制台查表 → 画字形"中"      ← 表在显示端，不在 char 里
```

**编码 = 编号 → 字节（写文件）；解码 = 字节 → 编号（读文件）。**  
`new String(bytes, UTF_8)` 走的是**解码**。

#### ② 必须记住的几个数字
| 数字 | 含义 |
| --- | --- |
| `65536`（`0x10000`） | BMP 的容量，也是 1 个 char 能表示的值的数量 |
| `0x10FFFF` | Unicode 码点上限（= 1114111） |
| `0xD800 ~ 0xDBFF` | 高位代理（**保留**，正常字符不落这里） |
| `0xDC00 ~ 0xDFFF` | 低位代理（同上） |
| `17` | 平面总数（BMP 是第 0 个） |
| `1 ~ 16` | 这些平面里的字符都要 **2 个 char** |


**代理对拆法**：码点 − `0x10000` → 补到 20 位 → 高 10 位 + `0xD800`、低 10 位 + `0xDC00`。

#### ③ 整型家族（`char` 是唯一的无符号）
| 类型 | 位数 | 有符号 | 范围 |
| --- | --- | --- | --- |
| `byte` | 8 | ✅ | −128 ~ 127 |
| `char` | 16 | ❌ **无** | 0 ~ 65535 |
| `short` | 16 | ✅ | −32768 ~ 32767 |
| `int` | 32 | ✅ | 约 ±21 亿 |


`char` 无符号，是因为它只装编号、不做算术。

#### ④ `String` 的 coder：**0 和 1**
| coder 值 | 名字 | 每个 char 占 |
| --- | --- | --- |
| **0** | `LATIN1` | 1 字节 |
| **1** | `UTF16` | 2 字节 |


只要字符串里有**一个** char 值 > 255，整个串升级成 `UTF16`（coder=1），英文数字也跟着变 2 字节 —— 有点浪费，但仍比“所有串都用 char[]”省。

#### ⑤ 一句话链
```plain
文件里的字节  --解码-->  码点  --存进-->  char 序列  --压缩存储-->  byte[] + coder
```

**逻辑上 String 是 char 序列（对外契约），物理上是 byte[] + coder（内存优化）。**  
压缩只改“每个 char 占几字节”，不改 char 的数量和值。

#### ⑥ 常用 API 的坑
| 需求 | 该用 | 不该用 |
| --- | --- | --- |
| 字符个数（真字数） | `codePointCount(0, s.length())` | `length()`（那是 char 数） |
| 第 i 个字的码点 | `codePointAt(i)` | `charAt(i)`（可能拿到半个 emoji） |
| 取片段 | `substring` | —— |


`"A😀中"`：`length()` = **4**，`codePointCount()` = **3**。

#### ⑦ UTF-8 的四种字节模式（复述时最容易写乱的一处）
| 总字节数 | 模式 | 数据位 |
| --- | --- | --- |
| 1 | `0xxxxxxx` | 7 |
| 2 | `110xxxxx 10xxxxxx` | 5 + 6 = 11 |
| 3 | `1110xxxx 10xxxxxx 10xxxxxx` | 4 + 6 + 6 = 16 |
| 4 | `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx` | 3 + 6 + 6 + 6 = 21 |


**两条规则，记这两条就够**：

1. **首字节开头有几个 **`**1**`**，总共就占几个字节**（`0` 开头=1 字节，`110`=2，`1110`=3，`11110`=4）；
2. **所有续字节一律以 **`**10**`** 开头**，无一例外。

**实拆 **`**中**`（UTF-8 = `E4 B8 AD`）：

```plain
E4 = 1110 0100   ← 1110 开头 → 总共 3 字节
B8 = 1011 1000   ← 10 开头 → 续字节 ✅
AD = 1010 1101   ← 10 开头 → 续字节 ✅
```

去掉标记位，把数据位拼起来：`0100` + `111000` + `101101` = `0x4E2D` = 20013 = `中` 的码点。

**常见写错**：把"1 的个数"当成"字节内容"（比如写成 `11110 1110 110 10`）。**标记位是固定的前缀，数据位紧跟在后面**，两者不分开写。

