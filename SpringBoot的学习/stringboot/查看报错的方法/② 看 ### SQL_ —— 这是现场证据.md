---
title: ② 看 ### SQL: —— 这是现场证据
url: https://www.yuque.com/ehsuh/pggizs/sowz18ik9q3xdod7
doc_id: 284835912
exported_at: 2026-09-12T09:41:00
---

```java
### SQL: SELECT  id,username,password,create_time  FROM user

```

**<font style="color:rgba(0, 0, 0, 0.9);">这就是 MyBatis 替你生成的 SQL</font>**<font style="color:rgba(0, 0, 0, 0.9);">——你一行 SQL 没写，它老老实实拼出来了。我前几轮说"不是没有 SQL，是框架替你写了"，这就是铁证 </font><font style="color:rgba(0, 0, 0, 0.9);">✅</font>

<font style="color:rgba(0, 0, 0, 0.9);">以后写复杂查询出错时，</font>**<font style="color:rgba(0, 0, 0, 0.9);">先把这行 SQL 复制到 Navicat 里跑一遍</font>**<font style="color:rgba(0, 0, 0, 0.9);">——SQL 在数据库里跑不通，那问题在 SQL；跑得通，那问题在 Java 这边。这一招能省掉一半的排查时间。</font>

