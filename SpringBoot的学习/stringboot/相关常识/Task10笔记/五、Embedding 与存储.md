---
title: 五、Embedding 与存储
url: https://www.yuque.com/ehsuh/pggizs/qtg0fzipc6129et7
doc_id: 290613260
exported_at: 2026-11-04T19:32:05
---

### 5.1 一句话原理
**embedding 把一段文字变成一串数字**，这串数字代表"**这段话在语义空间里的坐标**"。意思相近，坐标就靠。

**实测（余弦相似度）**：

| 对比 | 字面重合 | cosine |
| --- | --- | --- |
| "怎么重置密码" vs "忘记密码了怎么办" | **0 个字** | **0.8149** |
| "Spring Boot 自动配置" vs "SpringBoot 的自动装配机制" | 部分 | 0.7952 |
| "怎么重置密码" vs "今天天气真不错" | 0 | 0.2348 |


**第一行就是 RAG 的意义**：一个字都不重合，但它是同一件事。**关键词搜索永远找不到，向量能。**

### 5.2 存储：`SimpleVectorStore`（内存库）
```plain
// 内部结构（反编译看的）
final class SimpleVectorStoreContent {
    private final String id;                      // 唯一标识
    private final String text;                    // 块原文
    private final Map<String, Object> metadata;   // 元数据
    private final float[] embedding;              // 1024 维向量
}
protected Map<String, SimpleVectorStoreContent> store;   // key = id
```

**不是"两个 list 靠索引对应"，是一个 Map**：

+ `List` 靠**位置**关联 → 位置一错，静默出错
+ `Map` 靠 **id** 关联 → 天然成对

### 5.3 实测数据
```plain
块数 138（Task6 32 / Task8 54 / Task9 52）
向量化：逐条调 API，106 ms/条 → 138 块约 15 秒
加上启动 2.9 秒 → 每次启动约 15~18 秒
```

**代价**：内存库**重启就没了** → 每次启动都要重建。

**临时解法**：`SimpleVectorStore` 自带 `save(File)` / `load(File)`。 **生产解法**：持久化向量库（Redis Stack / Milvus / pgvector / Qdrant）。

⚠️ 向量文件是**产物**，不进 git：体积大、每次重建都变。放 `data/` 并加进 `.gitignore`。

