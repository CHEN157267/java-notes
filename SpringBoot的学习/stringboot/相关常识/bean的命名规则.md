---
title: bean的命名规则
url: https://www.yuque.com/ehsuh/pggizs/pbui1r0grka5cpa9
doc_id: 285544082
exported_at: 2026-09-17T22:25:37
---

**Spring 明文规定：实现类的对象的名字，是实现类的名字的首字母小写版。**

```java
@Service
public class UserServiceImpl implements UserService { }
//        ↓ Spring 自动给它起名
//     bean 名 = "userServiceImpl"      ← 类名首字母小写

@Qualifier("userServiceImpl")           // ← 所以这里要写这个名字

```

规则细分：

准确叫法是 **JavaBeans 的 **`**decapitalize**`**（首字母小写化）**

| **类名** | **bean 名** | **说明** |
| --- | --- | --- |
| `UserServiceImpl` | `userServiceImpl` | 常规：首字母变小写 |
| `URLService` | `URLService` | **前两个字母都是大写 → 原样不动** |
| `UUserService` | `UUserService` | 同上 |


为什么有特例？怕你写个 `URLService` 被变成 `uRLService` 太难看，所以约定"前两个字母都大写就不动"。





手动给bean命名

+ 想自己起名，就写 `@Service("userSvc")` → bean 名变成 `userSvc`，那 `@Qualifier` 也得跟着写 `"userSvc"`。

