---
title: 配置pom依赖的常见错误
url: https://www.yuque.com/ehsuh/pggizs/ia65pg0ir3x74g8r
doc_id: 289216566
exported_at: 2026-10-22T23:47:27
---

| 错误写法 | Maven 报什么 |
| --- | --- |
| 把 `<spring-ai.version>` 塞进 <br/>`<dependency>` 里 | `Unrecognised tag: 'spring-ai.version'` |
| `artifactId` 写成 `spring-ai`<br/>（不存在的名字） | `version is missing`（其实是因为找不到该 artifact） |
| 引用写成 `{$spring-ai.version}` | 不替换（符号写反了） |


