---
title: Task13 自测题 · 登录接口
url: https://www.yuque.com/ehsuh/pggizs/on3pdcaovt5ch9bg
doc_id: 292985631
exported_at: 2026-11-25T18:20:21
---

## 一、BCrypt 与密码校验（32 分）
### Q1（10 分）
为什么不能用这条 SQL 查用户？

```plain
SELECT * FROM user WHERE username = ? AND password = ?
```

**要说清"为什么必然失败"**，不能只说"因为加密了"。

---

### Q2（12 分）
`bCryptPasswordEncoder.matches(明文, 哈希串)` 内部做了哪三步？

（提示：想想盐在哪、谁把盐取出来的。）

---

### Q3（10 分）
下面这段代码为什么也查不到？（和 Q1 的错误不一样）

```plain
String hash = encoder.encode(password);      // 先把用户输入加密
userMapper.selectOne(new QueryWrapper<User>()
        .eq("username", username)
        .eq("password", hash));              // 再拿去比
```

---

## 二、安全边界（24 分）
### Q4（12 分）
"用户名不存在"和"密码错误"，为什么必须返回**一模一样**的提示？

+ 分开返回，攻击者能获得什么信息？
+ 这个手法叫什么名字？

---

### Q5（12 分）
登录失败时，下面两行日志哪一行可以写？为什么？

```plain
// A
log.warn("登录失败: username={}, password={}", username, password);

// B
log.warn("登录失败: username={}", username);
```

---

## 三、数据库约束（24 分）
### Q6（12 分）
表上已经有主键 `id`（保证每行唯一），为什么还需要 `username` 上的唯一索引？

+ 这两者分别保证什么？
+ 举一个"主键没问题、但业务出问题"的例子。

---

### Q7（12 分）
`addUser` 里已经有"先查是否存在，再插入"的逻辑，为什么还要加数据库唯一索引？

+ 什么情况下应用层的检查会失效？
+ 那时数据库会抛什么异常？

---

## 四、接口设计（20 分）
### Q8（10 分）
登录接口为什么用 `POST`，而不是：

+ `GET`？
+ `PUT`？

**两个都要说理由。**

---

### Q9（10 分）
登录接口的入参为什么单独建 `LoginRequest`，而不直接用 `User` 实体？

（说两条理由。）

---

## 附加题（不计分，但我要看）
`User` 实体的 `password` 字段上有 `@TableField(select = false)`。

它在**哪两个场景**下，一个帮了你、一个坑了你？各自怎么解决？

