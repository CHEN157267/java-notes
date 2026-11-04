---
title: 三、★ 两个 ChatModel 打架（必须记住的配置）
url: https://www.yuque.com/ehsuh/pggizs/sago626agaum3k0u
doc_id: 290739375
exported_at: 2026-11-04T19:32:04
---

加了 `spring-ai-starter-model-openai` 之后，**启动直接失败**：

```plain
APPLICATION FAILED TO START
Description:
  - deepSeekChatModel (DeepSeekChatAutoConfiguration)
  - openAiChatModel  (OpenAiChatAutoConfiguration)
Action: Consider marking one of the beans as @Primary...
```

**根因**（字节码里挖出来的）：

```plain
@ConditionalOnProperty(
    name = "spring.ai.model.chat",
    havingValue = "deepseek",
    matchIfMissing = true      // ← 不设置就等于启用
)
```

`**matchIfMissing = true**`** 意味着：不配置 = 两家都注册** → 两个 `ChatModel` bean → 注入时不知道选谁。

**解法**（properties 里两行）：

```plain
spring.ai.model.chat=deepseek
spring.ai.model.embedding=openai
```

### 配套的 base-url 坑
```plain
spring.ai.openai.embedding.base-url=https://llm-xxx.cn-beijing.maas.aliyuncs.com/compatible-mode
```

**末尾不能带 **`**/v1**`。因为 Spring AI 默认 `embeddings-path=/v1/embeddings`，它会自己补：

```plain
正确：.../compatible-mode + /v1/embeddings = .../compatible-mode/v1/embeddings  ✅
写错：.../compatible-mode/v1 + /v1/embeddings = .../v1/v1/embeddings           ❌ 404
```

