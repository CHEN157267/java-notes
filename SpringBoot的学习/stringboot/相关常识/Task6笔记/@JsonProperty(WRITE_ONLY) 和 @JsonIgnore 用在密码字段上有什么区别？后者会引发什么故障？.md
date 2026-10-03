---
title: @JsonProperty(WRITE_ONLY) 和 @JsonIgnore 用在密码字段上有什么区别？后者会引发什么故障？
url: https://www.yuque.com/ehsuh/pggizs/zhbumyp9zdqaooxn
doc_id: 248105939
exported_at: 2026-10-03T22:20:29
---

| 注解 | 进来的 password | 出去的 password | 结果 |
| --- | --- | --- | --- |
| `@JsonProperty(access = WRITE_ONLY)` | ✅ **保留** | ❌ 被丢弃 | ✅ 正确 |
| `@JsonIgnore` | ❌ **被丢弃** | ❌ 被丢弃 | ❌ **add 接口彻底用不了** |


`**@JsonIgnore**`** 是"双向全禁"——它连"进来"也一起掐掉。**

**故障链**：

```plain
前端 POST 带 password 的 JSON
   ↓ Jackson 看到 @JsonIgnore，直接【忽略】该字段，不往对象里塞
user.password  →  null
   ↓ 【★ 校验在门前，比 Service 早】
@NotBlank 拦下 → 400「密码不能为空」
```

**一个用户都建不出来。—— 前端传的密码永远进不来，永远卡在校验这一步。**

****

password 上标着 `@NotBlank`，而**校验发生在参数绑定阶段、比 Service 早**，所以你看到的**恰恰就是 notblank 的那句 message**（400「密码不能为空」），根本走不到 `encode(null)`。 只有在 password **没有**`@NotBlank` 的情况下，才会走到 `encode(null)` → 抛异常 → 500。

**这也顺便说明：**`**@JsonIgnore**`** 造成的现象是"字段变 null"，至于接下来报什么错、在哪一层报，取决于你在该字段上还标了什么别的注解。**

****

**一句话记牢**：`**@JsonIgnore**`** 说"这条路不走"，**`**WRITE_ONLY**`** 说"只走进来的方向"。** 密码要的是后者 —— **进得来、出不去。**

### ★ "读 / 写"是站在谁的角度
**站在服务端（Java 对象）的角度**，描述的是 **JSON 数据的流向**：

| 词 | 完整意思 | 方向 |
| --- | --- | --- |
| **WRITE** | 从 JSON **写入** Java 对象 | **进来**（前端 → 对象，反序列化） |
| **READ** | 从 Java 对象 **读出**、生成 JSON | **出去**（对象 → 前端，序列化） |


所以 `WRITE_ONLY` = **只许进、不许出**。

### ⚠️ 本轮两处要拧
**① 以为 **`**@JsonIgnore**`** 是标记给"不需要用户赋值 / 有默认值"的字段用的 —— 不是。**

它的准确语义是：**切断该字段的 JSON 通道**（进来、出去都不走）。

**关键区分**：`@JsonIgnore` ≠ "这字段不用赋值"。它只是堵住了 **JSON 这一条路**，字段本身**照样能被赋值** —— Java 代码里 `user.setXxx()` 正常生效，MyBatis-Plus 读写数据库也正常。**跟"有没有默认值""用户要不要改"完全无关。**

**② 例子举偏了 —— 用 **`**@PathVariable**`** 举例不对。**

`@PathVariable` 接收的是**方法形参**，它**压根不经过 **`**User**`** 对象**，谈不上"把值填进了 password 字段"。

**真正体现"其他手段还能填"的例子，就在自己代码里**：

```plain
user.setPassword(passwordEncoder.encode(user.getPassword()));
```

**这一行完全不经过 JSON。** 就算给 password 标上 `@JsonIgnore`，这行照样执行、照样把密文塞进对象、照样写进库。

**精确表述**：`@JsonIgnore` 关掉的是"**Jackson 的 JSON 通道**"这一个口子。Java 代码赋值、JDBC 读写、`@RequestParam`/`@PathVariable` 接收形参……**全都不归它管。**

### 实测双向验证（本项目）
| 位置 | 内容 |
| --- | --- |
| **响应体** | `{"id":16,"username":"wp-proof-927","createTime":null}` ← **没有 password** |
| **数据库** | `$2a$10$ZHpJcWlHaQ5LSCJevQ7OWuXhpirFQVa1WCT7mEiuEYOGcmtYL0TmG` |


**进来畅通、出去被挡。** ✔







## @JsonIgnore 会被 @NotBlank 拦住吗？——会，但因果方向要理清
不是"@NotBlank 认识 @JsonIgnore"，而是 **@JsonIgnore 让 password 变成 null，@NotBlank 再按自己的规矩（null 不合法）拒绝它**。上面那张图就是这两条路。

关键在**阶段顺序**：先绑定、后校验。

**添加到对话**

| **阶段** | **谁在干活** | **发生什么** |
| --- | --- | --- |
| ① 参数绑定 | Jackson（反序列化） | `@JsonIgnore`<br/> 在这里就把 password **丢掉** → 字段是 null |
| ② 校验 | Hibernate Validator + 你的 `@Valid` | 看见 null → 抛 `MethodArgumentNotValidException`<br/> → 你的 400 |


这两步**是先后关系，不是竞争关系**——跟你上次学的"`@ExceptionHandler` 靠类型挑、不靠顺序"正好是一对：那里是"谁更匹配谁上"，这里是"谁先谁后，阶段固定"。

