---
title: 关于对@Mapper的理解
url: https://www.yuque.com/ehsuh/pggizs/zg0gwegpw4gvdvw5
doc_id: 285429583
exported_at: 2026-09-17T22:25:51
---

`Mapper`层中，被@Mapper注释标记的文件 是个 interface → MyBatis 在运行时用 JDK 动态代理生成了一个实现类 → Spring 把它当 bean 放进容器 → 你在 `UserServiceImpl` 里 `@Autowired UserMapper` 就能拿到它。

