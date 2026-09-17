---
title: QueryWrapper的使用
url: https://www.yuque.com/ehsuh/pggizs/vvgqfa5on97774l2
doc_id: 285548836
exported_at: 2026-09-17T22:25:50
---

`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">QueryWrapper</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 的官方定位叫 </font>**<font style="color:rgba(0, 0, 0, 0.9);">条件构造器</font>**<font style="color:rgba(0, 0, 0, 0.9);">，说白了就是 </font>**<font style="color:rgba(0, 0, 0, 0.9);">SQL 里 </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">WHERE</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> 那部分的 Java 写法</font>**<font style="color:rgba(0, 0, 0, 0.9);">：</font>

```java
你写的 Java                                   数据库看到的 SQL
new QueryWrapper<User>()                      （空条件）
  .eq("username", "zhangsan")          →      WHERE username = 'zhangsan'
  .gt("age", 18)                       →      AND age > 18
  .orderByDesc("id")                   →      ORDER BY id DESC

```

