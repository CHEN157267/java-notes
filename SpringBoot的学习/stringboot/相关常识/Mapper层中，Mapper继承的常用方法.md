---
title: Mapper层中，Mapper继承的常用方法
url: https://www.yuque.com/ehsuh/pggizs/lpr4db8ur9yt3l8r
doc_id: 285549087
exported_at: 2026-09-17T22:25:34
---

它们都在 `BaseMapper` 里，是 MyBatis-Plus 白送的：

| **方法** | **返回** | **特点** |
| --- | --- | --- |
| `selectCount(wrapper)` | `Long`<br/>（条数） | **查重最合适**，只看"有几条" |
| `selectList(wrapper)` | `List<User>` | 能拿到记录，判 `isEmpty()`<br/> 也行 |
| `selectOne(wrapper)` | `User`<br/>（单条） | ⚠️ **匹配到多条会抛异常**，查重场景**别用** |


查重推荐用 `**selectCount**`：

```java
Long count = userMapper.selectCount(wrapper);   // ← 返回类型是 Long，不是 int
if (count > 0) { ... }                          // ← 说明这个名字已经有人用了

```

