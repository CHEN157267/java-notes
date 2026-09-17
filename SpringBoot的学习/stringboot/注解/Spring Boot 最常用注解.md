---
title: Spring Boot 最常用注解
url: https://www.yuque.com/ehsuh/pggizs/ib55z0io8qom3dt5
doc_id: 284226688
exported_at: 2026-09-12T09:41:09
---

### 1. `@RestController`
+ 标记在**类**上
+ 告诉 Spring：“我是一个控制器类，专门处理浏览器发来的请求，返回的数据直接作为响应体（JSON）返回给前端”
+ 就像餐厅服务员：接单 → 上菜

### 2. `@RequestMapping`
+ 标记在**类**或**方法**上
+ 告诉 Spring：“这个类/方法处理哪个网址的请求”
+ 类上写 `/user`，方法上写 `/login`，实际路径 = `/user/login`
+ 路径是**相对于服务器根路径**的

```java
@RestController
@RequestMapping("/user")           // 类上的前缀
public class UserController {

    @RequestMapping("/login")     // 完整路径 = /user/login
    public String login() {
        return "登录成功";
    }

    @RequestMapping("")           // 完整路径 = /user（空字符串不追加）
    public String index() {
        return "用户模块首页";
    }
}
```



## 补充二：`@RequestMapping` 详细说明
### 类上的 `@RequestMapping` 是“前缀”，只对带有 `@RequestMapping` 的方法生效
看代码：

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/login")     // 完整路径 = /user/login
    public String login() {
        return "登录成功";
    }

    @RequestMapping("")           // 完整路径 = /user （空字符串，不追加）
    public String index() {
        return "用户模块首页";
    }

    // 没有 @RequestMapping，外部无法访问，类上的 /user 对它不起作用
    private boolean checkPassword(String password) {
        return password.length() >= 6;
    }
}
```

解释：

+ 类上的 `@RequestMapping("/user")` **只影响**类中那些**自己也标注了**** **`**@RequestMapping**`** ****的方法**。
+ 方法上的路径会拼接在类前缀后面：`/user` + `/login` = `/user/login`。
+ 方法上的 `@RequestMapping("")` 表示不追加任何子路径，完整路径就是类前缀 `/user`。
+ **没有 **`**@RequestMapping**`** 的方法**完全不受类前缀影响，它根本不对外暴露，外面无法通过 URL 访问。它只是内部辅助方法。

### 有 `@RequestMapping` vs 没有 `@RequestMapping`
| 类型 | 对外暴露 URL | 示例 |
| --- | --- | --- |
| 有 `@RequestMapping` | 暴露，浏览器可通过 URL 访问 | `@RequestMapping("/login")` |
| 没有 `@RequestMapping` | 不暴露，只能类内部调用 | `private boolean checkPassword(...)` |


所以类上的 `@RequestMapping` 不是给整个类“贴路径”，而是给类中所有**标注了**** **`**@RequestMapping**`** ****的方法**统一加前缀。

---

## 总结
+ `@Autowired`：自动注入 Bean，可标注字段、构造器、setter，默认按类型查找。
+ `@RequestMapping`：类上的作为路径前缀，只对带 `@RequestMapping` 的方法生效；方法上的决定具体路径；没有该注解的方法不对外暴露。





### 3. `@Autowired`
+ 标记在**字段/构造器/方法**上
+ 告诉 Spring：“我这个字段需要注入一个 Bean 对象，你从容器里找一个符合类型的给我，自动赋值”
+ 它**不创建对象**，只是拿来用

### 4. `@Component`
+ 标记在**类**上
+ 告诉 Spring：“我是一个普通的 Bean，请把我加入 Spring 容器管理”
+ `@Service`、`@Repository`、`@Controller` 内部都包含 `@Component` 的功能，只是语义更明确

