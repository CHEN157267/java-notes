---
title: Task10笔记
url: https://www.yuque.com/ehsuh/pggizs/gige5u4risl8n2ia
doc_id: 290527715
exported_at: 2026-11-04T19:32:02
---

## 本项目 RAG 全链路（一张图在脑子里）
```plain
启动
 ├─ RagConfig → 造 SimpleVectorStore（bean，单例）
 ├─ RagLoader.run()
 │    ├─ 读 3 篇 md（UTF-8）
 │    ├─ 按 ## / ### 切 → 138 块
 │    ├─ 每块 = parentTitle + 正文 + metadata(source/chunk_index/section)
 │    └─ vectorStore.add() → 逐条调 embedding（15 秒）
 └─ 启动完成

请求 GET /rag/ask?q=...&topK=5
 ├─ RagServiceImpl.ask()
 │    ├─ search(q, topK)
 │    │    ├─ similaritySearch → 问题向量化 → 遍历 138 块算余弦 → 排序 → 取前 5
 │    │    └─ 转成 List<RagHit>（带 content）
 │    ├─ 过滤 score >= 0.5；空了直接返回"没有相关内容"
 │    ├─ 拼 StringBuilder（【资料i】来源 + 正文 + 【问题】）
 │    └─ chatClient.prompt().system(...).user(...).call().content()
 └─ Result<String>
```



## 九、错题清单（本轮踩过的坑）
| # | 坑 | 症状 | 正解 |
| --- | --- | --- | --- |
| 1 | DeepSeek 没有 embeddings 接口 | 404 | 换阿里百炼，走 OpenAI 兼容模式 |
| 2 | 两个 ChatModel 打架 | 启动失败 | `spring.ai.model.chat=deepseek` |
| 3 | base-url 带了 `/v1` | 404（`/v1/v1/embeddings`） | 末尾不能带 `/v1` |
| 4 | 以为换标点能改块数 | 块数一个没变 | 块大小由 `chunkSize` 决定 |
| 5 | 中文 token 换算按 1.5 字 | 成本算高 3 倍 | **1 token ≈ 2 字** |
| 6 | `**preview**`** 喂模型** | 答非所问 | 必须用 `content` |
| 7 | `**chunk_index**`** 依赖框架** | 换切法后 NPE → 500 | 自己写 metadata |
| 8 | `**seq**`** 写成方法形参** | 每节序号重置为 0 | 删形参 / 写 `this.seq` |
| 9 | **分支不收敛到一个出口** | 同一块被 add 3 次 | 只留一个 `addChunk` |
| 10 | `split("## ")[0]` | 返回空串 | 用 `lines().findFirst()` |
| 11 | `text.split("## ")[2]` | 数组越界 | split 只有 2 个元素 |
| 12 | 方法忘写 `@GetMapping` | 404 | 注解必须有 |


---

## 十、速记表（贴显示器）
1. **chunk 是检索的最小单位** —— 切碎了，再好的模型也答不出。
2. **向量只负责找，不负责还原** —— 库里必须同时存原文。
3. `**(?m)**`** 让 **`**^**`** 认每一行；**`**(?=)**`** 不消耗字符** —— 一个改语义，一个不改结果。
4. **方法形参一旦同名，就会遮住字段** —— 想改字段就写 `this.xxx`。
5. **别依赖别人顺手给的元数据** —— 换实现就没了，还是 NPE 这种最难懂的形式。
6. **筛选分三层**：检索器阈值（0.0）→ topK（5）→ 业务阈值（0.5）。
7. **"没找到"是正常结果，不是异常** —— 判据是"程序能不能继续"。
8. **先造对象、再灌数据、最后才查** —— 单例保证"你塞的我看得见"。

---

## 十一、遗留与后续
| 事项 | 状态 |
| --- | --- |
| 向量持久化（`save/load` 或换 Redis/Milvus） | ⬜ 未做 |
| 分批 + 并发入库（现在逐条 106ms） | ⬜ 未做 |
| Rerank（重排模型，解决"分数不低但无关"） | ⬜ 超出本 Task 范围 |
| 前端页面 | ⬜ 未做（现在只有接口） |
| Tool Calling / NL2SQL（查库） | ⬜ 后续任务 |


