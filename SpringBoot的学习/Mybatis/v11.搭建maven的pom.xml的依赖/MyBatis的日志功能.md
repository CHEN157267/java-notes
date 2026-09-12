---
title: MyBatis的日志功能
url: https://www.yuque.com/ehsuh/pggizs/nlpkbmhybprdo9li
doc_id: 278763815
exported_at: 2026-09-12T09:41:25
---

它的作用是**把MyBatis内部的运行细节“打印出来”**，帮你排查问题。比如：

+ SQL语句有没有执行？执行的是哪条？（比如`insert into t_car (...) values (...)`）
+ 数据库返回了多少条数据？有没有报错（比如“主键冲突”“字段类型不匹配”）？
+ 参数传递是否正确？（比如你传的`name`是“比亚迪汉”，SQL里有没有拿到这个值？）



记录**数据库操作的细节**（SQL、参数、执行结果），是**应用级（数据库交互层）**的日志。

