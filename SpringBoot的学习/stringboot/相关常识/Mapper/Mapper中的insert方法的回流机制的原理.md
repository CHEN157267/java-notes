---
title: Mapper中的insert方法的回流机制的原理
url: https://www.yuque.com/ehsuh/pggizs/eglgoyid2gpfs9y3
doc_id: 285884397
exported_at: 2026-09-21T20:48:35
---

MyBatis 把对象字段拆成 SQL 参数  →  发给 MySQL

MySQL 执行完，回执：改了 1 行 + 主键 9

MyBatis 收到回执，把 9 写回到那个对象上





**回填 id 不是"通用能力"，是给主键专门开的一条路。**

****

判据就一句话：**没有它，这个对象还能不能用。**

+ **id** —— 没有它，这个 `user` 就是**废的**。它以后要 `updateById(user)`、`deleteById(id)`、`selectById(id)`，**全都靠它定位**。框架必须还给你，不还就是设计失误。
+ **createTime** —— 没有它，这个对象**照样能增删改查**。只是"前端看不到时间"而已，不影响它作为一个可操作对象存在。

所以这不是"漏了"，是**优先级不同**：一个是活命的，一个是锦上添花的。



 **回填本质上是"自增主键"这个设计带来的补丁。**

