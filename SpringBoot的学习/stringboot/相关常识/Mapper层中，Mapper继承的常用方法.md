---
title: Mapper层中，Mapper继承的常用方法
url: https://www.yuque.com/ehsuh/pggizs/lpr4db8ur9yt3l8r
doc_id: 285549087
exported_at: 2026-09-17T22:25:34
---

<font style="color:rgba(0, 0, 0, 0.9);">它们都在 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">BaseMapper</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 里，是 MyBatis-Plus 白送的：</font>

| **<font style="color:rgba(0, 0, 0, 0.9);">方法</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">返回</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">特点</font>** |
| --- | --- | --- |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">selectCount(wrapper)</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">Long</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">（条数）</font> | **<font style="color:rgba(0, 0, 0, 0.9);">查重最合适</font>**<font style="color:rgba(0, 0, 0, 0.9);">，只看"有几条"</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">selectList(wrapper)</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">List<User></font>` | <font style="color:rgba(0, 0, 0, 0.9);">能拿到记录，判</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">isEmpty()</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">也行</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">selectOne(wrapper)</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">User</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">（单条）</font> | <font style="color:rgba(0, 0, 0, 0.9);">⚠️</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>**<font style="color:rgba(0, 0, 0, 0.9);">匹配到多条会抛异常</font>**<font style="color:rgba(0, 0, 0, 0.9);">，查重场景</font>**<font style="color:rgba(0, 0, 0, 0.9);">别用</font>** |


<font style="color:rgba(0, 0, 0, 0.9);">查重推荐用 </font>`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">selectCount</font>**`<font style="color:rgba(0, 0, 0, 0.9);">：</font>

```java
Long count = userMapper.selectCount(wrapper);   // ← 返回类型是 Long，不是 int
if (count > 0) { ... }                          // ← 说明这个名字已经有人用了

```

