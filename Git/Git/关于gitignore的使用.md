---
title: 关于gitignore的使用
url: https://www.yuque.com/ehsuh/nslcik/nv0nmg2blcqmmzmv
doc_id: 284838373
exported_at: 2026-09-12T09:41:34
---

1.`*.xml`：任意层级下，只要文件名以 `.xml` 结尾就全忽略。`*.iml`、`*.log` 一模一样。

2.

## `XXX/`（没有开头斜杠）≠ "从根目录开始"
没有开头斜杠，意思是**任意层级都能匹配**：

+ 我写的 `target/` 会忽略：根目录的 `target/`，**也会**忽略 `src/main/target/`、`a/b/target/`……只要叫 target 的目录都中招。
+ 想"只在根目录忽略 target"，得写 `/target/`（加开头斜杠）。

3.

## `/XXX/`（开头有斜杠）**不是**跟上一行拼接
你以为 `/XXX/` 会接在前面 `CCC/` 后面、拼成 `根/CCC/XXX`——**这是错的，而且错得很关键**。

Git 每一行都是**独立、完整**的规则，它脑子里没有"段落"、也不会把两行拼起来。开头的 `/` 只有一个意思：

**“从这个**** **`**.gitignore**`** ****文件自己所在的文件夹开始算”** 

+ 写在**根** `.gitignore` 里：`/target/` = 项目根/target
+ 写在 `**.idea/**` `.gitignore` 里：`/shelf/` = `.idea/shelf`

| **写法** | **开头有**** **`**/**`<br/>**？** | **含义** | **我们项目里举例** |
| --- | :---: | --- | --- |
| `target/` | 否 | 任意层级下叫 target 的目录 | 根/target、src/.../target 都忽略 |
| `/target/` | 是 | **仅本 gitignore 所在目录**下的 target | 根里写 = 项目根/target |
| `*.iml` | 否 | 任意层级、任意名的 .iml 文件 | 忽略所有 .iml |
| `/shelf/` | 是 | 仅本目录下的 shelf | `.idea/.gitignore`<br/> 里 = `.idea/shelf` |


