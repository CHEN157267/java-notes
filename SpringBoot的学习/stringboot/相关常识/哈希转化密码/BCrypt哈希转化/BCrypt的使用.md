---
title: BCrypt的使用
url: https://www.yuque.com/ehsuh/pggizs/xcgnhcw51se6tggf
doc_id: 256328824
exported_at: 2026-09-27T10:04:51
---

写在service层

```plain
private final BCryptPasswordEncoder passwordEncoder = new BCryptPasswordEncoder();
```

+ 它**无状态、线程安全** → 一个实例全局够用，**不必放进构造器**

****

+ `**encode()**`** 是纯函数****：****返回新字符串，不修改任何东西****。必须接住返回值：**

```plain
user.setPassword(passwordEncoder.encode(user.getPassword()));
```

| 方法 | 性格 |
| --- | --- |
| `encode(明文)` | **返回新值**，什么都不改（像 `+` 运算） |
| `setPassword(值)` | **就地修改**，返回 void |


只写 `passwordEncoder.encode(user.getPassword());` 单独一行 → 算出来的哈希**当场被丢掉**，库里存的还是明文。

+ **加密放在哪**：Service 层，**查重之后**
    - 理由：BCrypt 一次 100ms，让**必然失败**的请求提前返回，别白忙
    - Controller 只管收发；业务规则（"密码必须哈希"）归 Service

