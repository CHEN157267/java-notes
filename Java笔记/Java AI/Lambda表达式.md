---
title: Lambda表达式
url: https://www.yuque.com/ehsuh/oguki0/vsg04pipqwiraf9d
doc_id: 283817490
exported_at: 2026-09-12T10:37:14
---

1. Lambda 是什么？

一句话：把“一个接口只有一个抽象方法”的实现，简化成一行代码。

前提：只有函数式接口（只有一个抽象方法的接口）才能用 Lambda。比如 Comparator、Predicate、Consumer 这些都是函数式接口。





什么时候用 Lambda？

通常用在“需要一个接口实例，而且接口只有一个抽象方法”的地方。



```plain
(参数) -> { 方法体 }

```

与匿名内部类相比，他删去的更多，他删去了 new 类名或接口名(){方法名}，只剩下了方法的()和{}，且用箭头连接



规则：

· 参数类型可以省略（编译器自动推断）

· 一个参数可以省略小括号 ()

· 方法体只有一行，可以省略 {} 和 return





