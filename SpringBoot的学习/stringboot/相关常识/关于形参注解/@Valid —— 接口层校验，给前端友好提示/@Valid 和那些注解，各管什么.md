---
title: @Valid 和那些注解，各管什么
url: https://www.yuque.com/ehsuh/pggizs/zcv7bttpmyzs9fsu
doc_id: 286378245
exported_at: 2026-09-27T10:04:55
---

| 东西 | 写在哪 | 作用 |
| --- | --- | --- |
| `@NotBlank` / `@Pattern` / `@Size` | `User` 类的**字段**上 | **规则**（什么算合格） |
| `@Valid` | Controller 的**形参**上 | **开关**（请对这个对象跑一遍它自带的规则） |


+ `@Valid` **自身不含任何规则**，它只是个**触发器**。
+ 真正跑规则的是 **Hibernate Validator**（由 `spring-boot-starter-validation` 依赖带入）。
+ Spring MVC 里负责调它的是 `HandlerMethodArgumentResolver`（参数解析器）。
+ 所有校验注解对 `null` 都**放行**（只有 `@NotNull` / `@NotEmpty` / `@NotBlank` 例外），所以密码配了 `@Pattern` 也还得配 `@NotBlank`。

