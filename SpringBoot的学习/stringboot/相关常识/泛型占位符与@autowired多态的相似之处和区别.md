---
title: 泛型占位符与@autowired多态的相似之处和区别
url: https://www.yuque.com/ehsuh/pggizs/qkminv9mzn9oza8g
doc_id: 285545138
exported_at: 2026-09-17T22:25:36
---

**两者都让你"在不知道具体是谁的情况下就能写代码"**。

+ 泛型：我不用知道是 `User` 还是 `Order`，我照写 `list.get(0)`；
+ 多态：我不用知道背后是 `UserServiceImpl` 还是缓存版，我照调 `userService.getUser()`。

**共同的哲学叫「面向抽象编程」**——只不过一个抽象的是"**类型还没定 “，一个抽象的是” 实现还没定**"。这两个"没定"是不同层次的事，所以不能混。

