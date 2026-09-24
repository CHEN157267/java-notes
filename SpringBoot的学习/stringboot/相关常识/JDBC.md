---
title: JDBC
url: https://www.yuque.com/ehsuh/pggizs/cg1t3xgpvn7bsi97
doc_id: 286118017
exported_at: 2026-09-24T19:26:32
---

JDBC = **Java Database Connectivity**

+ **JDBC 是"接口规范"** —— 只规定"必须要有哪些方法"，**自己没有实现、不干活**

| "连接 Java 和 sql 的桥梁" | ✅ 方向对。更准的词是**标准 / 接口规范**；真正干活的那座"桥"是**驱动** |
| --- | --- |
| |  |
| "规范其他跟 Java 和 sql 有关的 jar 包" | ✅ 说对了 —— 它规范的就是**驱动 jar** |


实现 JDBC 的那个 jar **不是 Spring 出的**，是**数据库厂商**出的（`com.mysql.cj.jdbc.Driver` 是 MySQL 官方给的）。所以换个数据库，Java 代码不用动，只换厂商的 jar。

