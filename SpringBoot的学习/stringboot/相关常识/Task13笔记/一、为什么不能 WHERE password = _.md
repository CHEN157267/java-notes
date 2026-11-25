---
title: 一、为什么不能 WHERE password = ?
url: https://www.yuque.com/ehsuh/pggizs/imvaig44h3spyctm
doc_id: 293051938
exported_at: 2026-11-25T18:20:16
---

这是几乎所有人第一反应会写的：

```plain
SELECT * FROM user WHERE username = ? AND password = ?
```

**永远查不到。** 原因三层，一层比一层深：

### 1.1 库里是哈希，传进来的是明文
```plain
-- 库里            -- 传进来的
$2a$10$4X9sf...    123456
```

等值比较永远不成立。

### 1.2 “那我把输入也加密一次再比”——也不行
```plain
String hash = encoder.encode(password);   // $2a$10$AAA...
// 库里                          // $2a$10$BBB...
```

**因为每次 **`**encode**`** 都会生成一个全新的随机盐**，同一个密码两次结果完全不同。

### 1.3 唯一正确的做法：用那把盐重算
```plain
User user = userMapper.selectForLogin(username);
if (user == null || !encoder.matches(password, user.getPassword())) { ... }
```

---

