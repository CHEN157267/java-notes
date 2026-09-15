---
title: RESTful
url: https://www.yuque.com/ehsuh/pggizs/bxnieh2dy2bbg27y
doc_id: 285156093
exported_at: 2026-09-15T10:12:19
---

**<font style="color:rgba(0, 0, 0, 0.9);">用 URL 表示"东西"（名词），用 HTTP 方法表示"对它干什么"（动词）。</font>**

| **<font style="color:rgba(0, 0, 0, 0.9);">URL 长什么样</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">特点</font>** | |
| --- | --- | --- |
| **<font style="color:rgba(0, 0, 0, 0.9);">严格 REST</font>** | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">GET /users</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">POST /users</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">PUT /users/4</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">DELETE /users/4</font>` | <font style="color:rgba(0, 0, 0, 0.9);">URL 里</font>**<font style="color:rgba(0, 0, 0, 0.9);">只有名词</font>**<font style="color:rgba(0, 0, 0, 0.9);">，动作全靠 HTTP 方法表达</font> |
| **<font style="color:rgba(0, 0, 0, 0.9);">你的写法（通俗版）</font>** | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/user/list</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/user/add</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/user/update</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">/user/delete/{id}</font>` | <font style="color:rgba(0, 0, 0, 0.9);">URL 里</font>**<font style="color:rgba(0, 0, 0, 0.9);">带了动词</font>**<font style="color:rgba(0, 0, 0, 0.9);">，一看就懂，工程里极常见</font> |


