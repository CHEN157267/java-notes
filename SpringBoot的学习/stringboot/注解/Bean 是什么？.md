---
title: Bean 是什么？
url: https://www.yuque.com/ehsuh/pggizs/calraxxtdhndw6nb
doc_id: 284227106
exported_at: 2026-09-12T09:41:08
---

**<font style="color:rgb(15, 17, 21);">Bean 就是被 Spring 容器管理的对象。</font>**

+ <font style="color:rgb(15, 17, 21);">Spring 启动时，扫描所有标注了</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Component</font>`<font style="color:rgb(15, 17, 21);">（及</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Service</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Repository</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Controller</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">等）的类</font>
+ <font style="color:rgb(15, 17, 21);">自动创建这些类的对象，放进一个容器里</font>
+ <font style="color:rgb(15, 17, 21);">以后想用某个对象，不用自己 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">new</font>`<font style="color:rgb(15, 17, 21);">，用 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Autowired</font>`<font style="color:rgb(15, 17, 21);"> 从容器里取</font>

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

