---
title: 关于@Controller相关的注释细节
url: https://www.yuque.com/ehsuh/pggizs/chbhzl0ff9wdz07o
doc_id: 284933930
exported_at: 2026-09-15T10:12:26
---

+ `**@RestController**`** 是个"组合注解"**，它 = `**@Controller**`** + **`**@ResponseBody**`。
    - `@Controller` 这部分 → 负责"把类注册成一个控制器 bean"（你朋友说的就是这半句）；
    - `@ResponseBody` 这部分 → 负责"这个类的每个方法返回值都直接写进响应体（默认转 JSON），而不是当视图名去渲染网页"。
    - `**@Controller**`** 本身也会生成 bean**，区别只在于：它的方法默认**返回视图名**（去渲染 HTML 页面，比如 JSP/Thymeleaf）；而 `@RestController` 因为带了 `@ResponseBody`，方法默认**返回数据**（JSON）

| **注解** | **生成 bean？** | **方法返回默认是** | **典型用途** |
| --- | --- | --- | --- |
| `@Controller` | ✅ | 视图名（HTML 页面） | 传统 MVC、要返回网页 |
| `@RestController` | ✅ | 数据（JSON/XML） | 前后端分离的接口 API |


