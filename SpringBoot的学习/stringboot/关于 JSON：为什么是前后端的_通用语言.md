---
title: 关于 JSON：为什么是前后端的"通用语言
url: https://www.yuque.com/ehsuh/pggizs/vlk2t0s0xfqnuhmr
doc_id: 284932866
exported_at: 2026-09-15T10:12:25
---

+ **JSON 不是"JavaScript 的改写版"**。它全称 _JavaScript Object Notation_，语法**借用了** JS 对象字面量的写法（花括号、键值对、数组），但它**只是一种文本数据格式**，不是 JavaScript 代码，不能执行。
+ **为什么它能成为通用语言**，核心原因是三点：
    1. **前端是 JS，而 JS 原生就能解析 JSON**（`JSON.parse()` 自带），前后端一拍即合；
    2. **它是纯文本、语言无关**——Java / Python / Go 任何后端都能轻松序列化和反序列化，等于大家都能"说"这门语言；
    3. **比 XML 轻**——同样的用户信息，JSON 字符数少、结构清晰，网络传输更省。、

总结：**JSON 因为"前端 JS 天生认识 + 后端全员能解析 + 格式轻"，才成了前后端之间约定俗成的数据交换格式。** 你用的 `@RequestBody`/`@ResponseBody` 就是 Spring 帮你做"Java 对象 ↔ JSON 文本"双向翻译的翻译官。

