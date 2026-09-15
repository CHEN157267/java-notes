---
title: 关于@Controller相关的注释细节
url: https://www.yuque.com/ehsuh/pggizs/chbhzl0ff9wdz07o
doc_id: 284933930
exported_at: 2026-09-15T10:12:26
---

+ `**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@RestController</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> 是个"组合注解"</font>**<font style="color:rgba(0, 0, 0, 0.9);">，它 = </font>`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Controller</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> + </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@ResponseBody</font>**`<font style="color:rgba(0, 0, 0, 0.9);">。</font>
    - `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Controller</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">这部分 → 负责"把类注册成一个控制器 bean"（你朋友说的就是这半句）；</font>
    - `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@ResponseBody</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 这部分 → 负责"这个类的每个方法返回值都直接写进响应体（默认转 JSON），而不是当视图名去渲染网页"。</font>
    - `**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Controller</font>**`**<font style="color:rgba(0, 0, 0, 0.9);"> 本身也会生成 bean</font>**<font style="color:rgba(0, 0, 0, 0.9);">，区别只在于：它的方法默认</font>**<font style="color:rgba(0, 0, 0, 0.9);">返回视图名</font>**<font style="color:rgba(0, 0, 0, 0.9);">（去渲染 HTML 页面，比如 JSP/Thymeleaf）；而 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@RestController</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 因为带了 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@ResponseBody</font>`<font style="color:rgba(0, 0, 0, 0.9);">，方法默认</font>**<font style="color:rgba(0, 0, 0, 0.9);">返回数据</font>**<font style="color:rgba(0, 0, 0, 0.9);">（JSON）</font>

| **<font style="color:rgba(0, 0, 0, 0.9);">注解</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">生成 bean？</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">方法返回默认是</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">典型用途</font>** |
| --- | --- | --- | --- |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Controller</font>` | <font style="color:rgba(0, 0, 0, 0.9);">✅</font> | <font style="color:rgba(0, 0, 0, 0.9);">视图名（HTML 页面）</font> | <font style="color:rgba(0, 0, 0, 0.9);">传统 MVC、要返回网页</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@RestController</font>` | <font style="color:rgba(0, 0, 0, 0.9);">✅</font> | <font style="color:rgba(0, 0, 0, 0.9);">数据（JSON/XML）</font> | <font style="color:rgba(0, 0, 0, 0.9);">前后端分离的接口 API</font> |


