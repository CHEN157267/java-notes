---
title: 泛型占位符与@autowired多态的相似之处和区别
url: https://www.yuque.com/ehsuh/pggizs/qkminv9mzn9oza8g
doc_id: 285545138
exported_at: 2026-09-17T22:25:36
---

**<font style="color:rgba(0, 0, 0, 0.9);">两者都让你"在不知道具体是谁的情况下就能写代码"</font>**<font style="color:rgba(0, 0, 0, 0.9);">。</font>

+ <font style="color:rgba(0, 0, 0, 0.9);">泛型：我不用知道是</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">User</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">还是</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">Order</font>`<font style="color:rgba(0, 0, 0, 0.9);">，我照写</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">list.get(0)</font>`<font style="color:rgba(0, 0, 0, 0.9);">；</font>
+ <font style="color:rgba(0, 0, 0, 0.9);">多态：我不用知道背后是 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 还是缓存版，我照调 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">userService.getUser()</font>`<font style="color:rgba(0, 0, 0, 0.9);">。</font>

**<font style="color:rgba(0, 0, 0, 0.9);">共同的哲学叫「面向抽象编程」</font>**<font style="color:rgba(0, 0, 0, 0.9);">——只不过一个抽象的是"</font>**<font style="color:rgba(0, 0, 0, 0.9);">类型还没定 “，一个抽象的是” 实现还没定</font>**<font style="color:rgba(0, 0, 0, 0.9);">"。这两个"没定"是不同层次的事，所以不能混。</font>

