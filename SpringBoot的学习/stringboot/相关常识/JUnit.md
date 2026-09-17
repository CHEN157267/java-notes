---
title: JUnit
url: https://www.yuque.com/ehsuh/pggizs/webob60d59b0pufs
doc_id: 285419908
exported_at: 2026-09-17T22:25:47
---

+ 跑这个测试时，JUnit 只加载相关的类，**不启动 Tomcat、不走 HTTP，脱离的是"Web 层"，不是"Spring"**。
+ `@SpringBootTest` **仍会启动 Spring 容器**（所以 Service、Mapper 才能被注入），只是**不启动内嵌 Tomcat、不走 HTTP 链路**。
+ 如果方法只涉及纯逻辑（比如算个值），连数据库都不用连；
+ 如果方法里调了 mapper（查库），就加 `@SpringBootTest` 让 Spring 把 Service、Mapper 都注入好再测。

