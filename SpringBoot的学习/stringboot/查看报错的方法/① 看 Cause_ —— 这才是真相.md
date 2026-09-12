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

<font style="color:rgba(0, 0, 0, 0.9);">规律：</font>**<font style="color:rgba(0, 0, 0, 0.9);">一层层 </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">Cause:</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> 往下剥，最里面那个才是真凶</font>**<font style="color:rgba(0, 0, 0, 0.9);">。外面的 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">BadSqlGrammarException</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 只是 Spring 给它套的"包装盒"。</font>

