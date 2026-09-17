---
title: 控制器（Controller）
url: https://www.yuque.com/ehsuh/pggizs/mg2be6h6weg1ewky
doc_id: 284228006
exported_at: 2026-09-12T09:41:07
---

+   
被 `@RestController` 标记的类就是控制器
+ 负责**接收用户请求、调用业务逻辑、返回数据**
+ 按模块划分，可以有多个控制器（不是像 main 方法只有一个）
+ 控制器里不是所有方法都有 `@RequestMapping`，没有的只是内部辅助方法，外部无法访问

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/register")
    public String register(String username, String password) {
        if (checkPassword(password)) {       // 调用内部方法
            return "注册成功";
        }
        return "密码太短";
    }

    // 没有 @RequestMapping，外部无法访问，只是内部辅助
    private boolean checkPassword(String password) {
        return password.length() >= 6;
    }
}
```

**有 **`**@RequestMapping**`：对外暴露 URL，浏览器可访问  
**没有 **`**@RequestMapping**`：内部辅助方法，封装重复逻辑，不让外部触碰

