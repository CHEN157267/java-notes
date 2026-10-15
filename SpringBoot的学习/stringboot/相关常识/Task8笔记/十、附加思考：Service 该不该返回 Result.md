---
title: 十、附加思考：Service 该不该返回 Result
url: https://www.yuque.com/ehsuh/pggizs/ox8bbza8d9q7qc68
doc_id: 288322429
exported_at: 2026-10-15T19:53:02
---

**好处（若 Service 返回 Result）**：Controller **变薄**（拿到就能 `return`，不用再包 `Result.success(...)`）；调用方**不用 try-catch**（失败也变成返回值）。**是个小便利。**

**真正的坏处**：**Service 被 web 概念污染**。

+ `Result` 是**给 HTTP 用的**（里面的 code 是"响应语义"）；
+ 但 Service 以后会被**非 web 的地方**复用：**定时任务、消息队列消费者、另一个服务**——那些场景**根本没有"返回给前端"这回事**，却被逼着处理一个 web 响应对象，别扭且易误解。
+ 职责上：**Controller 的活就是"翻译"**（把 Service 的结果翻译成 HTTP 响应）。让 Service 直接产出 Result，等于**越权**。

**结论：选 **`**void**`**（+ 失败抛异常）**，跟真实项目主流做法一致。

**Service 说业务语言，Controller 说 HTTP 语言。**



