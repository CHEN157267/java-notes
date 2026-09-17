---
title: 使用String regex和Pattern p = Pattern.compile(regex);的区别
url: https://www.yuque.com/ehsuh/oguki0/rxpck55hndn6g8ce
doc_id: 219073752
exported_at: 2026-09-12T10:38:23
---

`Matcher`对象是通过`Pattern`对象的`matcher()`方法来创建的。`Pattern`类表示正则表达式的编译表示，先使用`Pattern.compile(String regex)`方法将正则表达式字符串编译成`Pattern`对象，然后再通过这个`Pattern`对象调用`matcher()`方法，并传入要匹配的文本字符串，才能创建出`Matcher`对象 。



**直接使用**`**String**`**的局限性**：单纯的`String`类型只是存储了正则表达式的文本内容，它没有具备编译正则表达式以及执行匹配操作的能力。而`Matcher`类需要基于已经编译好的正则表达式模式（即`Pattern`对象 ）来对目标文本进行匹配工作 。

