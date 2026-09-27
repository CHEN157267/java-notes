---
title: 校验失败之后，message 到底在哪
url: https://www.yuque.com/ehsuh/pggizs/yg04oeaik9t996vb
doc_id: 286378292
exported_at: 2026-09-27T10:04:56
---

**message 一直都在，但默认情况下前端拿不到它。**

| 位置 | 有没有 message | 说明 |
| --- | --- | --- |
| 异常对象里 | ✅ **有** | `MethodArgumentNotValidException` 的 `FieldError.getDefaultMessage()` —— 这是**源头** |
| 服务端 WARN 日志里 | ✅ **有** | IDEA 控制台搜 `Validation failed` 就能看到；**不管有没有 advice，日志都会打** |
| HTTP 响应体里 | ❌ **没有** | 默认只有 `{timestamp, status, error, path}` 四个字段 |


默认响应体长这样（A5 实测，102 字节）：

```plain

```

**这不是 Spring 忘了带，是故意的**：默认错误页刻意隐藏服务端内部细节，防止信息外泄。安全设计。

用词注意：处理器取 message 是**从异常对象里取**，不是"从日志里捞"。 日志是**输出**（打印出来的副本），它只是你能亲眼看到"message 还在"的证据。

