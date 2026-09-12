---
title: 关于gitignore的使用
url: https://www.yuque.com/ehsuh/nslcik/nv0nmg2blcqmmzmv
doc_id: 284838373
exported_at: 2026-09-12T09:41:34
---

1.`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">*.xml</font>`<font style="color:rgba(0, 0, 0, 0.9);">：任意层级下，只要文件名以 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.xml</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 结尾就全忽略。</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">*.iml</font>`<font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">*.log</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 一模一样。</font>

<font style="color:rgba(0, 0, 0, 0.9);">2.</font>

## `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">XXX/</font>`<font style="color:rgba(0, 0, 0, 0.9);">（没有开头斜杠）≠ "从根目录开始"</font>
<font style="color:rgba(0, 0, 0, 0.9);">没有开头斜杠，意思是</font>**<font style="color:rgba(0, 0, 0, 0.9);">任意层级都能匹配</font>**<font style="color:rgba(0, 0, 0, 0.9);">：</font>

+ <font style="color:rgba(0, 0, 0, 0.9);">我写的</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">target/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">会忽略：根目录的</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">target/</font>`<font style="color:rgba(0, 0, 0, 0.9);">，</font>**<font style="color:rgba(0, 0, 0, 0.9);">也会</font>**<font style="color:rgba(0, 0, 0, 0.9);">忽略</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">src/main/target/</font>`<font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">a/b/target/</font>`<font style="color:rgba(0, 0, 0, 0.9);">……只要叫 target 的目录都中招。</font>
+ <font style="color:rgba(0, 0, 0, 0.9);">想"只在根目录忽略 target"，得写 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/target/</font>`<font style="color:rgba(0, 0, 0, 0.9);">（加开头斜杠）。</font>

<font style="color:rgba(0, 0, 0, 0.9);">3.</font>

## `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/XXX/</font>`<font style="color:rgba(0, 0, 0, 0.9);">（开头有斜杠）</font>**<font style="color:rgba(0, 0, 0, 0.9);">不是</font>**<font style="color:rgba(0, 0, 0, 0.9);">跟上一行拼接</font>
<font style="color:rgba(0, 0, 0, 0.9);">你以为</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/XXX/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">会接在前面</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">CCC/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">后面、拼成</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">根/CCC/XXX</font>`<font style="color:rgba(0, 0, 0, 0.9);">——</font>**<font style="color:rgba(0, 0, 0, 0.9);">这是错的，而且错得很关键</font>**<font style="color:rgba(0, 0, 0, 0.9);">。</font>

<font style="color:rgba(0, 0, 0, 0.9);">Git 每一行都是</font>**<font style="color:rgba(0, 0, 0, 0.9);">独立、完整</font>**<font style="color:rgba(0, 0, 0, 0.9);">的规则，它脑子里没有"段落"、也不会把两行拼起来。开头的</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">只有一个意思：</font>

**<font style="color:rgba(0, 0, 0, 0.9);">“从这个</font>****<font style="color:rgba(0, 0, 0, 0.9);"> </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.gitignore</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> </font>****<font style="color:rgba(0, 0, 0, 0.9);">文件自己所在的文件夹开始算”</font>**<font style="color:rgba(0, 0, 0, 0.9);"> </font>

+ <font style="color:rgba(0, 0, 0, 0.9);">写在</font>**<font style="color:rgba(0, 0, 0, 0.9);">根</font>**<font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.gitignore</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">里：</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/target/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">= 项目根/target</font>
+ <font style="color:rgba(0, 0, 0, 0.9);">写在 </font>`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.idea/</font>**`<font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.gitignore</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 里：</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/shelf/</font>`<font style="color:rgba(0, 0, 0, 0.9);"> = </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.idea/shelf</font>`

| **<font style="color:rgba(0, 0, 0, 0.9);">写法</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">开头有</font>****<font style="color:rgba(0, 0, 0, 0.9);"> </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/</font>**`<br/>**<font style="color:rgba(0, 0, 0, 0.9);">？</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">含义</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">我们项目里举例</font>** |
| --- | :---: | --- | --- |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">target/</font>` | <font style="color:rgba(0, 0, 0, 0.9);">否</font> | <font style="color:rgba(0, 0, 0, 0.9);">任意层级下叫 target 的目录</font> | <font style="color:rgba(0, 0, 0, 0.9);">根/target、src/.../target 都忽略</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/target/</font>` | <font style="color:rgba(0, 0, 0, 0.9);">是</font> | **<font style="color:rgba(0, 0, 0, 0.9);">仅本 gitignore 所在目录</font>**<font style="color:rgba(0, 0, 0, 0.9);">下的 target</font> | <font style="color:rgba(0, 0, 0, 0.9);">根里写 = 项目根/target</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">*.iml</font>` | <font style="color:rgba(0, 0, 0, 0.9);">否</font> | <font style="color:rgba(0, 0, 0, 0.9);">任意层级、任意名的 .iml 文件</font> | <font style="color:rgba(0, 0, 0, 0.9);">忽略所有 .iml</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/shelf/</font>` | <font style="color:rgba(0, 0, 0, 0.9);">是</font> | <font style="color:rgba(0, 0, 0, 0.9);">仅本目录下的 shelf</font> | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.idea/.gitignore</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">里 =</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">.idea/shelf</font>` |


