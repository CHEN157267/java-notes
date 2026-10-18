---
title: application.properties
url: https://www.yuque.com/ehsuh/pggizs/rvmsbqzgo93r0d1b
doc_id: 288657513
exported_at: 2026-10-18T10:06:26
---

**  
它和 pom 是"两个阶段"的配置**：

| | **pom.xml** | **application.properties** |
| --- | --- | --- |
| 管什么 | **依赖 + 构建**（要哪些 jar、怎么编译打包） | **应用怎么跑**（连哪个库、端口、密钥、开关） |
| 何时生效 | **构建期** | **运行期** |
| 类比 | 装修的**材料清单** | 电器的**旋钮设置** |


机制：**Spring Boot 启动时读它，把 **`**key=value**`** 塞进 Environment**，各处再用 `${}` / 自动配置取值。

