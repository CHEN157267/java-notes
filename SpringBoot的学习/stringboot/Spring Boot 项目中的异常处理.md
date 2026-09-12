---
title: Spring Boot 项目中的异常处理
url: https://www.yuque.com/ehsuh/pggizs/hyl84es4bfhdrqwy
doc_id: 284087602
exported_at: 2026-09-12T09:41:10
---

**<font style="color:rgb(15, 17, 21);">问：Spring Boot 项目里业务代码很少写 try-catch，是真的吗？异常都去哪了？</font>**

<font style="color:rgb(15, 17, 21);">答：</font>

1. <font style="color:rgb(15, 17, 21);">是真的，业务代码通常不写 try-catch，而是直接 throws 或者让运行时异常自然抛出。</font>
2. <font style="color:rgb(15, 17, 21);">这些异常会被框架的全局异常处理器（</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@ControllerAdvice</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">+</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@ExceptionHandler</font>`<font style="color:rgb(15, 17, 21);">）统一捕获。</font>
3. <font style="color:rgb(15, 17, 21);">全局处理器记录日志并返回统一格式的错误响应给前端，业务代码更干净。</font>

