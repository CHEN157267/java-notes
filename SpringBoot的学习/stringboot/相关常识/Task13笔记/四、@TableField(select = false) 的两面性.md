---
title: 四、@TableField(select = false) 的两面性
url: https://www.yuque.com/ehsuh/pggizs/uevkvnevwymsv14r
doc_id: 293052949
exported_at: 2026-11-25T18:20:18
---

### 4.1 它让登录查不到密码
```plain
User user = userMapper.selectOne(new QueryWrapper<User>().eq("username", username));
// user.getPassword() == null   ← 因为 SQL 根本不查这一列
// → matches 返回 false → 密码正确也登不进去
```

**表现**：`401 用户名或密码错误`，但密码明明是对的。

### 4.2 解决：`@Select` 手写 SQL
```plain
@Select("SELECT id, username, password, create_time FROM user WHERE username = #{username}")
User selectForLogin(@Param("username") String username);
```

**为什么能绕过**：`@TableField` 只影响 **MyBatis-Plus 自动拼 SQL** 的时候；手写 SQL 它管不着。

`@Param("username")` 的作用：把方法参数绑定到 SQL 里的 `#{username}` 占位符。**跟数据库列名无关**（列名是 SQL 里直接写的）。

### 4.3 ⚠️ 一条重要的澄清：动机 ≠ 现状
“`@TableField(select=false)` 帮忙的场景是 SQL 日志不打印密码”——**这句话是错的**，至少现在不成立。

**时间线**：

| 时间 | 发生了什么 |
| --- | --- |
| 11-07 | 加这个注解，动机：SQL 日志别把密码刷到控制台 |
| **11-20** | **注释掉 **`**log-impl=StdOutImpl**`（它连结果集都打，更危险） |
| 现在 | “防日志”的价值**已经消失**，只剩“默认查询不带这列” |


**代码加上去时的理由，可能因为别处的改动而失效。**

### 4.4 三层注解各管一段
| 注解 | 管什么 | 坑在哪 |
| --- | --- | --- |
| `@TableField(select=false)` | 查库时不取这列 | **登录拿不到哈希** |
| `@JsonProperty(WRITE_ONLY)` | 转 JSON 时不输出 | 不影响查库 |
| `@JsonIgnore` | 双向都忽略 | 前端传的密码收不到，`@NotBlank` 直接 400 |


