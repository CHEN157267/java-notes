---
title: ③with root cause（根因）
url: https://www.yuque.com/ehsuh/pggizs/tgfte8grviupsg3a
doc_id: 284836068
exported_at: 2026-09-12T09:40:59
---

<font style="color:rgba(0, 0, 0, 0.9);">那是从 Java 底层到你的代码的</font>**<font style="color:rgba(0, 0, 0, 0.9);">调用栈</font>**<font style="color:rgba(0, 0, 0, 0.9);">（HikariCP 连接池 → JDBC 驱动 → MySQL），是给框架开发者看的。</font>**<font style="color:rgba(0, 0, 0, 0.9);">你只需要最下面那行 </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">with root cause</font>**`**<font style="color:rgba(0, 0, 0, 0.9);">（根因）就够了。</font>**

<font style="color:rgba(0, 0, 0, 0.9);">顺带认识两个老面孔：</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">mysql-connector-j-9.7.0.jar</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">是</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>**<font style="color:rgba(0, 0, 0, 0.9);">MySQL 驱动</font>**<font style="color:rgba(0, 0, 0, 0.9);">（JDBC 的实现），</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">HikariCP</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">是</font>**<font style="color:rgba(0, 0, 0, 0.9);">数据库连接池</font>**<font style="color:rgba(0, 0, 0, 0.9);">（Spring Boot 默认用它管理连接）。</font>

**<font style="color:rgba(0, 0, 0, 0.9);">  
</font>****<font style="color:rgba(0, 0, 0, 0.9);"> </font>**

