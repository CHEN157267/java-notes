---
title: 兜底方法返回 String 会出现什么问题？为什么换 Result<Void> 就好了？
url: https://www.yuque.com/ehsuh/pggizs/bzv4sr30sxt5oo71
doc_id: 255769102
exported_at: 2026-10-03T22:20:30
---

**不会编译失败、不会报错 —— 是"能返回"的。** 但**格式变了**：

| 返回类型 | 谁负责序列化 | 结果 |
| --- | --- | --- |
| `Result<Void>` | **Jackson** | `application/json` ✅ |
| `String` | `StringHttpMessageConverter` | `**text/plain**` ❌ |


**后果**：响应体是光秃秃一句 `系统繁忙，请稍后重试` —— **没有 **`**code**`**、没有 **`**data**`，`Content-Type` 变成 `text/plain`，**前端按 JSON 一解析就炸**。

**完整链条**：

```plain
返回值类型  →  挑一个能处理它的 HttpMessageConverter  →  决定 Content-Type  →  写进响应体
```

### ⚠️ 本轮答偏的地方：因果反了
| 我的说法 | 正解 |
| --- | --- |
| "因为是 `@RestController` 标记的控制器，**所以**它返回的就是 JSON" | `**@RestController**`** 不决定格式。** |


`**@RestController**`** 只做一件事**：保证**返回值写进响应体**（而不是被当成"要跳转的页面名"）。 **至于写成什么格式**，是 Spring 手里一排**消息转换器（**`**HttpMessageConverter**`**）**在竞争，**按返回类型挑一个能处理它的**。

**响应体只有一个**（就是这次 HTTP 响应），不是"有好几种响应体让它选"。真正有多个候选的是**转换器**。

**准确表述**： 「`@RestController` 保证了返回值会进响应体；但在返回 `String` 时，被选中的转换器是纯文本转换器，于是输出 `text/plain`，与前端期望的 JSON 不符。」

