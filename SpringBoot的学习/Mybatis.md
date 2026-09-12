---
title: Mybatis
url: https://www.yuque.com/ehsuh/pggizs/aqw2tgr17fx7icyl
doc_id: 277130688
exported_at: 2026-09-12T09:41:18
---

<!-- 这是一张图片，ocr 内容为：1.4.MYBATIS简介 MYBATIS是一款优秀的持久层框架,它极大地方便了JAVA程序与数据库的交互.它的核心特点包括: 1.彻底解放JDBC编码 完全避免了手动设置参数,处理结果集等重复性JDBC代码 .极大简化了数据库交互的编程模型 2.SQL与代码分离 .支持XML和注解两种开发方式,其中XML方式因其灵活性成为主流选择 .实现业务逻辑与数据访问逻辑的彻底解耦,代码结构更清晰 3.灵活的SQL定制能力 提供基本映射,高级映射和动态SQL标签 允许编写精确优化的SQL语句,保持完全的SQL控制权 4.简洁的ORM映射 将JAVA接口和简单POJO对象自动映射为数据库记录 架构轻量,学习成本低,仅需少量依赖配置即可快速上手 -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783667232689-2f0acf9b-45bf-4162-b70f-15cd6a9d74bf.png)



MyBatis 还有其他功能，不是只干跟数据库有关的活

+ 缓存机制（一级缓存、二级缓存）
+ 延迟加载
+ 动态 SQL 拼接
+ 插件机制（分页插件等）所以 MyBatis 本身的 jar 包必须是 `compile`，因为你写代码时就要 `import`它的类。

