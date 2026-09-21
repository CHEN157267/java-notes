---
title: MyBatis-Plus 条件构造器（Wrapper）
url: https://www.yuque.com/ehsuh/pggizs/gvbhw9tptmohy55e
doc_id: 286006302
exported_at: 2026-09-21T23:02:35
---

Wrapper 是你写给 MyBatis-Plus 的**条件清单**。 你只管一个一个写条件，**连接词（AND / OR）由它负责翻译**。

```plain
new QueryWrapper<User>()
    .eq("username", "zhangsan")
    .ne("id", 1)
```

翻译结果（这一步是框架做的，不是你写的）：

```plain
WHERE username = 'zhangsan' AND id != 1
```

**中间那个 AND 不用你写。**

---

## 常用条件方法
第一个参数永远是**数据库列名**（字符串形式），第二个是值。

| 方法 | 含义 | 生成的 SQL | 示例 |
| --- | --- | --- | --- |
| `eq` | 等于 | `col = ?` | `.eq("username", "zhangsan")` |
| `ne` | 不等于 | `col <> ?` | `.ne("id", 1)` |
| `gt` | 大于 | `col > ?` | `.gt("create_time", "2026-01-01")` |
| `ge` | 大于等于 | `col >= ?` | `.ge("id", 10)` |
| `lt` | 小于 | `col < ?` | `.lt("id", 100)` |
| `le` | 小于等于 | `col <= ?` | `.le("id", 100)` |
| `like` | 包含（两边模糊） | `col LIKE '%?%'` | `.like("username", "zhang")` |
| `likeRight` | 以…开头 | `col LIKE '?%'` | `.likeRight("username", "zhang")` |
| `isNull` | 为空 | `col IS NULL` | `.isNull("password")` |
| `isNotNull` | 不为空 | `col IS NOT NULL` | `.isNotNull("username")` |
| `in` | 在列表中 | `col IN (?,?,?)` | `.in("id", 1, 2, 3)` |
| `notIn` | 不在列表中 | `col NOT IN (?,?)` | `.notIn("id", 1, 2)` |
| `between` | 区间（含两端） | `col BETWEEN ? AND ?` | `.between("id", 1, 10)` |
| `orderByAsc` | 升序 | `ORDER BY col ASC` | `.orderByAsc("id")` |
| `orderByDesc` | 降序 | `ORDER BY col DESC` | `.orderByDesc("create_time")` |


---

## ★ 多条件怎么连（重点）
### 默认就是 AND
```plain
.eq("username", "zhangsan")
.gt("id", 5)
.likeRight("password", "a")
```

→ `WHERE username = 'zhangsan' AND id > 5 AND password LIKE 'a%'`

**接几个条件就有几个 AND，你一个 AND 字都不用打。**

### 要 OR 才需要自己写
```plain
.eq("username", "zhangsan").or().eq("username", "lisi")
```

→ `WHERE username = 'zhangsan' OR username = 'lisi'`

`.or()` 就是插在中间的那个"转折点"。

### 混合 AND / OR
从左往右依次生效，容易出错。真需要时用括号分组（`.and(w -> ...)` 这种，属进阶，先不碰）。

---

## 综合示例
```plain
// 用户名以 zhang 开头，且 create_time 在 2026 年之后，按 id 倒序
QueryWrapper<User> qw = new QueryWrapper<User>()
        .likeRight("username", "zhang")
        .gt("create_time", "2026-01-01")
        .orderByDesc("id");
```

对应 SQL：

```plain
SELECT * FROM user
WHERE username LIKE 'zhang%' AND create_time > '2026-01-01'
ORDER BY id DESC
```

## 两种 Wrapper
| | 列名怎么写 | 特点 |
| --- | --- | --- |
| `QueryWrapper` | 字符串：`"create_time"` | 现在在用；**列名写错要到运行时才发现** |
| `LambdaQueryWrapper` | 方法引用：`User::getCreateTime` | 写错**编译期就报红**，更安全，以后可以换 |


常见坑

1. 列名写"数据库列名"，不是 Java 字段名  
.eq("create_time", ...) ✅ ／ .eq("createTime", ...) ❌  
（用 Lambda 版就没这问题）
2. 传 null 值是静默坑  
.eq("username", null) 会拼出 username = null，SQL 里恒不成立 → 不报错，但什么都查不到。  
要判空请用 .isNull("username")。
3. .last() 慎用  
它把字符串直接拼到 SQL 末尾，用不好有注入风险。
4. updateById 会跳过 null 字段  
所以它没法把某字段改成 null（想做要用 UpdateWrapper 显式 set）。

