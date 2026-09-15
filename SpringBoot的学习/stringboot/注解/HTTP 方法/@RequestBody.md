---
title: @RequestBody
url: https://www.yuque.com/ehsuh/pggizs/td589pu8oq83i2h6
doc_id: 284931192
exported_at: 2026-09-15T10:12:27
---

<font style="color:rgba(0, 0, 0, 0.9);">@RequestBody的作用就是告诉 Spring "这个参数从</font>**<font style="color:rgba(0, 0, 0, 0.9);">请求体</font>**<font style="color:rgba(0, 0, 0, 0.9);">里拿，并且按 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">Content-Type</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 选择对应消息转换器（常见为 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">application/json</font>`<font style="color:rgba(0, 0, 0, 0.9);">）把请求体反序列化成对象"。</font>

<font style="color:rgba(0, 0, 0, 0.9);">简单来说，@RequestBody的作用就是接收到网页的JSON数据之后，有这个</font>**<font style="color:rgba(0, 0, 0, 0.9);">注解的形参</font>**<font style="color:rgba(0, 0, 0, 0.9);">代表让spring把网页接收的JSON数据或其它类型的数据转化为Java对应的类的对象</font>

