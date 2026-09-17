---
title: ① 看 Cause: —— 这才是真相
url: https://www.yuque.com/ehsuh/pggizs/bkfq0k5kmniwrkax
doc_id: 284835877
exported_at: 2026-09-12T09:41:01
---

```java
Cause: java.sql.SQLSyntaxErrorException: Table 'demo_db.user' doesn't exist
;Cause: 真正的错误原因
;SQLSyntaxErrorException: SQL 语法/对象类错误（表不存在、列名写错都归它管）

```

规律：**一层层 **`**Cause:**`** 往下剥，最里面那个才是真凶**。外面的 `BadSqlGrammarException` 只是 Spring 给它套的"包装盒"。

