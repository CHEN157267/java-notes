---
title: RESTful
url: https://www.yuque.com/ehsuh/pggizs/bxnieh2dy2bbg27y
doc_id: 285156093
exported_at: 2026-09-15T10:12:19
---

**用 URL 表示"东西"（名词），用 HTTP 方法表示"对它干什么"（动词）。**

| **URL 长什么样** | **特点** | |
| --- | --- | --- |
| **严格 REST** | `GET /users`<br/>、`POST /users`<br/>、`PUT /users/4`<br/>、`DELETE /users/4` | URL 里**只有名词**，动作全靠 HTTP 方法表达 |
| **你的写法（通俗版）** | `/user/list`<br/>、`/user/add`<br/>、`/user/update`<br/>、`/user/delete/{id}` | URL 里**带了动词**，一看就懂，工程里极常见 |


