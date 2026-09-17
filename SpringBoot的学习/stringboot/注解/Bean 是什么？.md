---
title: Bean 是什么？
url: https://www.yuque.com/ehsuh/pggizs/calraxxtdhndw6nb
doc_id: 284227106
exported_at: 2026-09-12T09:41:08
---

**Bean 就是被 Spring 容器管理的对象。**

+ Spring 启动时，扫描所有标注了 `@Component`（及 `@Service`、`@Repository`、`@Controller` 等）的类
+ 自动创建这些类的对象，放进一个容器里
+ 以后想用某个对象，不用自己 `new`，用 `@Autowired` 从容器里取

```java
@Component
public class UserService {
    public void register() {
        System.out.println("用户注册");
    }
}

@RestController
public class OrderController {
    @Autowired
    private UserService userService;   // Spring 自动从容器里取 UserService 对象注入

    @RequestMapping("/order")
    public String createOrder() {
        userService.register();        // 直接使用
        return "下单成功";
    }
}
```

