---
title: 六、检索：similaritySearch 内部做了什么
url: https://www.yuque.com/ehsuh/pggizs/qxfpqnzwypc3d7ti
doc_id: 290613314
exported_at: 2026-11-04T19:32:06
---

源码原文（`SimpleVectorStore.doSimilaritySearch`）：

```plain
float[] userQueryEmbedding = getUserQueryEmbedding(request.getQuery());   // ① 问题也向量化

return this.store.values().stream()
    .map(content -> content.toDocument(
        EmbeddingMath.cosineSimilarity(userQueryEmbedding, content.getEmbedding())  // ② 逐条算余弦
    ))
    .filter(doc -> doc.getScore() >= request.getSimilarityThreshold())    // ③ 低于阈值扔掉
    .sorted(Comparator.comparing(Document::getScore).reversed())          // ④ 按分数降序
    .limit(request.getTopK())                                             // ⑤ 取前 K
    .toList();
```

**它就是"遍历全部 + 逐个算余弦 + 排序取前 K"** —— 没有任何索引结构。

138 条无所谓；100 万条就慢死了 → 这就是生产要换 Milvus/Redis 的技术原因（它们有 **ANN 索引**：HNSW / IVF，百万级也是毫秒级）。

### 6.1 score 与 distance
```plain
score    相似度，越高越像，最高 1.0（实践中 0.6~0.8 就算很相关）
distance 距离，越低越像
关系     distance = 1 - score
```

### 6.2 三层筛选（很容易混）
| 层 | 名称 | 在哪 | 值 |
| --- | --- | --- | --- |
| 1 | `similarityThreshold` | `SearchRequest`（检索器内部） | 默认 **0.0**（不过滤） |
| 2 | `topK` | `SearchRequest`（取前 K） | 我们设 **5** |
| 3 | `scoreThreshold` | **我们自己 **`**ask()**`** 里** | **0.5** |


**前两个是"检索器参数"，第三个是"业务判断"。**

---

