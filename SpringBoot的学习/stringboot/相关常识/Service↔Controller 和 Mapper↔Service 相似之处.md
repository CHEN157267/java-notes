---
title: Service↔Controller 和 Mapper↔Service 相似之处
url: https://www.yuque.com/ehsuh/pggizs/qbmwy2hzhrdwk8p2
doc_id: 285480122
exported_at: 2026-09-17T22:25:42
---

**依赖方只写"接口"，实现对象由外部注入。**

+ **Service 层**：`UserController` 依赖 `UserService`（接口），实现 = `UserServiceImpl`（**你自己手写**）
+ **Mapper 层**：`UserServiceImpl` 依赖 `UserMapper`（接口），实现 = MyBatis 动态代理（**框架自动生成，你没写**）

**共同点**：两处都符合"面向接口 + 依赖注入"。  
**不同点（唯一的）**：**实现类是谁造的**——service层的实现类是你造，Mapper层的实现类是 MyBatis 造。

