---
title: ③with root cause（根因）
url: https://www.yuque.com/ehsuh/pggizs/tgfte8grviupsg3a
doc_id: 284836068
exported_at: 2026-09-12T09:40:59
---

那是从 Java 底层到你的代码的**调用栈**（HikariCP 连接池 → JDBC 驱动 → MySQL），是给框架开发者看的。**你只需要最下面那行 **`**with root cause**`**（根因）就够了。**

顺带认识两个老面孔：`mysql-connector-j-9.7.0.jar` 是 **MySQL 驱动**（JDBC 的实现），`HikariCP` 是**数据库连接池**（Spring Boot 默认用它管理连接）。

**  
**** **

