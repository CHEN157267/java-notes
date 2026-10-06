---
title: OpenAPI 文档注解（四层注解）
url: https://www.yuque.com/ehsuh/pggizs/cwf2ssozprel765r
doc_id: 287164665
exported_at: 2026-10-06T10:13:30
---

**  
添加到对话**

| **口语** | **全限定名** | **贴在哪** |
| --- | --- | --- |
| ① | `io.swagger.v3.oas.annotations.OpenAPIDefinition` | 启动类 |
| ② | `io.swagger.v3.oas.annotations.tags.Tag` | Controller 类 |
| ③ | `io.swagger.v3.oas.annotations.Operation` | 方法 |
| ④ | `io.swagger.v3.oas.annotations.media.Schema` | 类 / 字段 |


它们统一前缀是 `io.swagger.v3.oas.annotations`——**这一串就是"Swagger 的 OpenAPI v3 注解包"**。以后你写笔记，标题直接写"**OpenAPI 注解 “或” Swagger 文档注解**"



| 注解 | 贴哪 | 管什么 |
| --- | --- | --- |
| `@OpenAPIDefinition(info = @Info(...))` | 启动类 | 文档标题/版本 |
| `@Tag(name = "用户管理")` | Controller 类 | 左侧分组名 |
| `@Operation(summary = "...")` | 方法 | 接口中文说明 |
| `@Schema(description = "...")` | 类/字段 | 数据模型说明 |


---



`**@Info**`** 不能平级写**：因为 `@Info` 的 `@Target` 只有 `ANNOTATION_TYPE`，编译器从语言层面禁止它贴类上。判"独立注解 vs 成员"就看 `@Target`。

**Q5 · 名字两种身份**：显示名（`@Tag.name`，自己写，随便）vs 标识名（`ResultUser`，工具推导，受字符集约束）。`Result<User>` 不能当名字的**两个硬理由**：① 要当 `$ref` 的 URI 片段 ② 要当代码生成器的类名——都是"`<>` 不合规"

**Q7 · password 两条防线**：响应不出 password = Jackson（`@JsonProperty(WRITE_ONLY)`）；文档标 `writeOnly` = springdoc **自动读** Jackson 的注解翻译，不用额外写 `@Schema`。

