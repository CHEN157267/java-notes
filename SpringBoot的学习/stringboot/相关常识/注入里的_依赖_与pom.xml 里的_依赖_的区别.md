---
title: 注入里的"依赖"与pom.xml 里的"依赖"的区别
url: https://www.yuque.com/ehsuh/pggizs/oy1523le2do6n8i9
doc_id: 285484406
exported_at: 2026-09-17T22:25:40
---

| **   ****pom.xml 里的"依赖"** | **注入里的"依赖"** | |
| --- | --- | --- |
| 指的是 | **库/jar 包** | **一个对象** |
| 层面 | 编译期的**代码库** | 运行期的**对象** |
| 例子 | `spring-boot-starter-web`<br/>、`mybatis-plus` | `UserServiceImpl`<br/> 需要的 `UserMapper`<br/> 对象 |
| 你需要它的原因 | 我的**代码**要用别人的类 | 我的**对象**要另一个对象才能干活 |


共同点：

"**我自己干不了，得靠别人**"。



不同点：

pom 里写 `mybatis-plus`，是为了能用 `BaseMapper` 这些类；

DI 说的"依赖"，是运行时 `UserServiceImpl` 手里得握着一个 `UserMapper` 对象。

