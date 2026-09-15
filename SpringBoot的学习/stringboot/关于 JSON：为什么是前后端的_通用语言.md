---
title: 关于 JSON：为什么是前后端的"通用语言
url: https://www.yuque.com/ehsuh/pggizs/vlk2t0s0xfqnuhmr
doc_id: 284932866
exported_at: 2026-09-15T10:12:25
---

+ **<font style="color:rgba(0, 0, 0, 0.9);">JSON 不是"JavaScript 的改写版"</font>**<font style="color:rgba(0, 0, 0, 0.9);">。它全称 </font>_<font style="color:rgba(0, 0, 0, 0.9);">JavaScript Object Notation</font>_<font style="color:rgba(0, 0, 0, 0.9);">，语法</font>**<font style="color:rgba(0, 0, 0, 0.9);">借用了</font>**<font style="color:rgba(0, 0, 0, 0.9);"> JS 对象字面量的写法（花括号、键值对、数组），但它</font>**<font style="color:rgba(0, 0, 0, 0.9);">只是一种文本数据格式</font>**<font style="color:rgba(0, 0, 0, 0.9);">，不是 JavaScript 代码，不能执行。</font>
+ **<font style="color:rgba(0, 0, 0, 0.9);">为什么它能成为通用语言</font>**<font style="color:rgba(0, 0, 0, 0.9);">，核心原因是三点：</font>
    1. **<font style="color:rgba(0, 0, 0, 0.9);">前端是 JS，而 JS 原生就能解析 JSON</font>**<font style="color:rgba(0, 0, 0, 0.9);">（</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">JSON.parse()</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">自带），前后端一拍即合；</font>
    2. **<font style="color:rgba(0, 0, 0, 0.9);">它是纯文本、语言无关</font>**<font style="color:rgba(0, 0, 0, 0.9);">——Java / Python / Go 任何后端都能轻松序列化和反序列化，等于大家都能"说"这门语言；</font>
    3. **<font style="color:rgba(0, 0, 0, 0.9);">比 XML 轻</font>**<font style="color:rgba(0, 0, 0, 0.9);">——同样的用户信息，JSON 字符数少、结构清晰，网络传输更省。、</font>

总结：**<font style="color:rgba(0, 0, 0, 0.9);">JSON 因为"前端 JS 天生认识 + 后端全员能解析 + 格式轻"，才成了前后端之间约定俗成的数据交换格式。</font>**<font style="color:rgba(0, 0, 0, 0.9);"> 你用的 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@RequestBody</font>`<font style="color:rgba(0, 0, 0, 0.9);">/</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@ResponseBody</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 就是 Spring 帮你做"Java 对象 </font><font style="color:rgba(0, 0, 0, 0.9);">↔</font><font style="color:rgba(0, 0, 0, 0.9);"> JSON 文本"双向翻译的翻译官。</font>

