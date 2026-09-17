---
title: @RequestParam 还能接表单
url: https://www.yuque.com/ehsuh/pggizs/nr848nt73f2sg3rh
doc_id: 285156559
exported_at: 2026-09-15T10:12:22
---

**HTML 表单提交的数据，长的就是"键值对"**，而不是 JSON。

```java
<form method="post" action="/user/save">
  <input name="id" value="4">
  <input name="username" value="lisi">
</form>

```

点提交后，浏览器发的**请求体**长这样（**不是 JSON**）：

```java
id=4&username=lisi

```



