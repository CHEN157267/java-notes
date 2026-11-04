---
title: 四、切分：从「按 token 硬切」到「按标题切」
url: https://www.yuque.com/ehsuh/pggizs/gw9pvnwm9qy37pw1
doc_id: 290613032
exported_at: 2026-11-04T19:32:04
---

### 4.1 先说结论：**chunk 是检索的最小单位**
检索不是"找文档"，是"**找块**"。所以**怎么切，直接决定召回质量**。

**判据**：一个好的 chunk，是「**能被一个问题完整命中**」的最小单位。

### 4.2 `TokenTextSplitter` 到底怎么切（源码级）
```plain
List<Integer> chunk = tokens.subList(0, Math.min(chunkSize, tokens.size()));  // ① 先装满
String chunkText = decodeTokens(chunk);
if (tokens.size() > chunkSize) {
    int lastPunctuation = getLastPunctuationIndex(chunkText);                  // ② 往回找标点
    if (lastPunctuation != -1 && lastPunctuation > minChunkSizeChars) {
        chunkText = chunkText.substring(0, lastPunctuation + 1);               // ③ 从那里截断
    }
}
```

**关键：块有多大由 **`**chunkSize**`** 决定，标点只决定"结尾退到哪"。**

所以我们试过换中文标点集合（`。！？；`），**块数一个没变**（还是 11/17/13）—— 这就验证了这条。

### 4.3 两代切法的实测对比
| | 硬切 chunkSize=800 | 硬切 chunkSize=300 | **按标题切** |
| --- | --- | --- | --- |
| 总块数 | 41 | 112 | **138** |
| 平均块长 | 1519 字 | 554 字 | **450 字** |
| 块内语义 | 表格/句子从中断 | 仍然断 | **一节一块，完整** |
| Q6 能否召回 | ❌ | ❌ | ✅ |


**顺带纠正一个换算**：CL100K 对中文约 **1 token ≈ 2 个汉字**（不是 1.5）。

验证：`18118 字 ÷ 11 块 ÷ 800 token ≈ 2.06`，`24702 ÷ 17 ÷ 800 ≈ 1.82`，`19475 ÷ 13 ÷ 800 ≈ 1.87`。

### 4.4 按标题切的四个步骤
```plain
① 按 "## " 切      → 得到 N 个「节」（每节都以 ## 开头）
② 每节再按 "### " 切 → 得到 subs[]
③ 每个小节前面拼上它所属的「## 标题」  ← contextual header
④ 边界处理：太短的丢、太长的（>1200 字）用 TokenTextSplitter 二次切
```

**为什么第 ③ 步很重要**：`### 5.3 环境变量的名字和值，都不能有空格` 这行本身信息量够，但加上 `## 五、密钥管理` 之后，**"这块在讲什么"直接写进了正文**，向量就有了锚点。

⚠️ **必须拼进正文，不能放 metadata**：embedding 只看 `Document.getText()`，**metadata 完全不参与向量化**。

### 4.5 三个分支（核心逻辑）
```plain
// A：这节没有三级标题
if (subs.length == 1) {
    addChunk(subs[0]);      // 它自带 ## 标题，不拼
    return;                 // ★ 必须 return，否则会掉到 B 再 add 一次
}

// B：subs[0] = "## 标题 + 第一个 ### 之前的正文"
if (subs[0].length() > 60) {
    addChunk(subs[0]);      // 已自带标题，不拼
}

// C：从 1 开始，每个三级块拼上二级标题
for (int i = 1; i < subs.length; i++) {
    addChunk(parentTitle + "\n" + subs[i]);
}
```

**为什么 B 分支不能省**：Task9 里只有两节符合"`## 标题` 后面直接跟正文"，而这两节装的是**最关键的两张表**：

1. 「四、配置体系」408 字 —— `pom properties` vs `application.properties` 对照表
2. 「七、DeepSeek 的模型名」441 字 —— 12 tokens vs 156/206 tokens 实测表

**删掉 B，这两张表整块消失。**

**阈值为什么取 60**：纯标题段 **10~29 字**，有正文的 **408/441 字**，中间隔着一整个数量级。

### 4.6 两个正则的精确含义
```plain
content.split("(?m)^(?=## )")
```

| 符号 | 含义 | 去掉会怎样 |
| --- | --- | --- |
| `(?m)` | 多行模式：让 `^``$` 认**每一行**的首尾（默认只认整个字符串的首尾） | 只在开头切一刀，几乎切不动 |
| `(?=...)` | **零宽正向断言**：断言"这个位置后面是 `## `"，**但不消耗字符** | 改成 `^## ` → `## ` 被当分隔符**吃掉**，标题没了 |


`**split**`** 的固定行为：丢弃分隔符。** 所以：

```plain
"## 五、密钥管理\n...".split("## ")          →  ["", "五、密钥管理\n..."]   // [0] 是空串
"# H1\n## 五、密钥管理\n...".split("(?m)^(?=## )") → ["# H1", "## 五、密钥管理\n..."]  // 无空串
```

**两种写法会产生完全不同的首元素**——这是踩坑的根源之一。

