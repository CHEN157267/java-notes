---
title: 六、DeepSeek 的模型名
url: https://www.yuque.com/ehsuh/pggizs/ydau5din7kbmdq1h
doc_id: 289218828
exported_at: 2026-10-22T23:47:30
---

| 传入的 model | HTTP | 平台返回的 model | total_tokens | message 字段 |
| --- | --- | --- | --- | --- |
| `deepseek-chat` | 200 | `deepseek-flash` | **12 / 12** | content, role |
| `deepseek-flash` | 200 | `deepseek-flash` | **156 / 206** | content, role, `**reasoning_content**` |


### 结论
1. **两个名字都能用**，底层都是 **V4.1-Flash**
2. **真正的区别是"要不要思考过程"**
    - `deepseek-chat`：**不返回思考**（快、省）
    - `deepseek-flash`：**默认返回思考**（`reasoning_content`），token 是 10~17 倍
1. **选 **`**deepseek-chat**` —— 我们要的是"把答案返给用户"，不需要思考过程；而且不暴露思考内容**更安全**



### 5.x 补充：枚举里没有 flash，为什么还能配
`spring.ai.deepseek.chat.options.model` 的类型是 `**String**`，**透传**：

```plain
你配什么 → Spring AI 原样填进请求体的 "model" 字段 → 发给 DeepSeek
```

**Spring AI 不校验这个名字存不存在；能不能用由 DeepSeek 服务器决定。**

**角色分工**：

+ **Spring AI = 邮差**（只负责抄写和投递）
+ **DeepSeek = 收件人**（只有它知道哪个名字对应哪个模型）
+ **枚举 = 常用名字小抄**（方便你别拼错，**不是白名单**）

