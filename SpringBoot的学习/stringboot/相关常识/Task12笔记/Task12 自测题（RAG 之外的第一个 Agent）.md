---
title: Task12 自测题（RAG 之外的第一个 Agent）
url: https://www.yuque.com/ehsuh/pggizs/iwwqx1lfzm9g3b4u
doc_id: 292827301
exported_at: 2026-11-22T10:02:08
---

**Q1**（10 分）  
“模型执行 Java 方法”和“模型只输出调用意图”，区别是什么？用一句话说清楚。

**Q2**（10 分）  
`@Tool` 标在 A 类的方法上，但 `defaultTools` 里传的是 B 类的对象。运行时会发生什么？为什么？

**Q3**（15 分）  
模型返回的 `arguments = {"id": 4}` 里，**这个**** **`**4**`** ****是从哪来的**？  
（提示：不是我们代码填的）

**Q4**（15 分）  
一次工具调用会在日志里看到三段 messages：

```plain
① {role: USER,      content: "..."}
② {role: ASSISTANT, toolCalls: [...]}
③ {role: TOOL,      content: [...]}
```

这三段分别是**谁**写进去的？为什么第二次请求要带上前两段？

**Q5**（10 分）  
为什么 `addUser` / `updateUser` / `deleteUser` **不能**加 `@Tool`？  
你的答案要能解释“就算我真的加了，会有什么后果”。

**Q6**（10 分）  
`@Tool` 的 `description` 里，**应该写什么、不应该写什么**？举一个“写了不该写的”例子。

---

**附加题（不计分，但我要看）**

我们最后是用 `-Djava.net.preferIPv4Stack=true` 才连上 DeepSeek 的。你觉得**为什么 curl 能连通、Java 却连不上**？

