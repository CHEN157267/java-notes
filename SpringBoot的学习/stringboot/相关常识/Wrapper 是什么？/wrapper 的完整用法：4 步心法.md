---
title: wrapper 的完整用法：4 步心法
url: https://www.yuque.com/ehsuh/pggizs/mf5dzwzih42av6xd
doc_id: 285548942
exported_at: 2026-09-17T22:25:48
---

```java
// ① 造容器（泛型写你的实体类）
QueryWrapper<User> wrapper = new QueryWrapper<>();

// ② 往容器里塞条件（链式，可以一直点）
wrapper.eq("username", user.getUsername());   // WHERE username = ?
// 想加更多就继续：wrapper.like(...).orderByDesc("id");

// ③ 交给 mapper 去查
Long count = userMapper.selectCount(wrapper);

// ④ 用结果（判断 count > 0）

```

