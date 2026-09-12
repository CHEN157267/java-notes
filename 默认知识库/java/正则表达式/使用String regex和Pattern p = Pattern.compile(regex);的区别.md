---
title: 使用String regex和Pattern p = Pattern.compile(regex);的区别
url: https://www.yuque.com/ehsuh/oguki0/rxpck55hndn6g8ce
doc_id: 219073752
exported_at: 2026-09-12T09:40:11
---

`<font style="color:rgb(0, 0, 0);">Matcher</font>`<font style="color:rgba(0, 0, 0, 0.85);">对象是通过</font>`<font style="color:rgb(0, 0, 0);">Pattern</font>`<font style="color:rgba(0, 0, 0, 0.85);">对象的</font>`<font style="color:rgb(0, 0, 0);">matcher()</font>`<font style="color:rgba(0, 0, 0, 0.85);">方法来创建的。</font>`<font style="color:rgb(0, 0, 0);">Pattern</font>`<font style="color:rgba(0, 0, 0, 0.85);">类表示正则表达式的编译表示，先使用</font>`<font style="color:rgb(0, 0, 0);">Pattern.compile(String regex)</font>`<font style="color:rgba(0, 0, 0, 0.85);">方法将正则表达式字符串编译成</font>`<font style="color:rgb(0, 0, 0);">Pattern</font>`<font style="color:rgba(0, 0, 0, 0.85);">对象，然后再通过这个</font>`<font style="color:rgb(0, 0, 0);">Pattern</font>`<font style="color:rgba(0, 0, 0, 0.85);">对象调用</font>`<font style="color:rgb(0, 0, 0);">matcher()</font>`<font style="color:rgba(0, 0, 0, 0.85);">方法，并传入要匹配的文本字符串，才能创建出</font>`<font style="color:rgb(0, 0, 0);">Matcher</font>`<font style="color:rgba(0, 0, 0, 0.85);">对象 。</font>

<font style="color:rgba(0, 0, 0, 0.85);"></font>

**<font style="color:rgb(0, 0, 0) !important;">直接使用</font>**`**<font style="color:rgb(0, 0, 0);">String</font>**`**<font style="color:rgb(0, 0, 0) !important;">的局限性</font>**<font style="color:rgba(0, 0, 0, 0.85) !important;">：单纯的</font>`<font style="color:rgb(0, 0, 0);">String</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">类型只是存储了正则表达式的文本内容，它没有具备编译正则表达式以及执行匹配操作的能力。而</font>`<font style="color:rgb(0, 0, 0);">Matcher</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">类需要基于已经编译好的正则表达式模式（即</font>`<font style="color:rgb(0, 0, 0);">Pattern</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">对象 ）来对目标文本进行匹配工作 。</font>

