---
title: @RequestParam 还能接表单
url: https://www.yuque.com/ehsuh/pggizs/nr848nt73f2sg3rh
doc_id: 285156559
exported_at: 2026-09-15T10:12:22
---

**<font style="color:rgba(0, 0, 0, 0.9);">HTML 表单提交的数据，长的就是"键值对"</font>**<font style="color:rgba(0, 0, 0, 0.9);">，而不是 JSON。</font>

```java
<form method="post" action="/user/save">
  <input name="id" value="4">
  <input name="username" value="lisi">
</form>

```

<font style="color:rgba(0, 0, 0, 0.9);">点提交后，浏览器发的</font>**<font style="color:rgba(0, 0, 0, 0.9);">请求体</font>**<font style="color:rgba(0, 0, 0, 0.9);">长这样（</font>**<font style="color:rgba(0, 0, 0, 0.9);">不是 JSON</font>**<font style="color:rgba(0, 0, 0, 0.9);">）：</font>

```java
id=4&username=lisi

```



