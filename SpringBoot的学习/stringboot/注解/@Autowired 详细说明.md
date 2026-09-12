---
title: @Autowired 详细说明
url: https://www.yuque.com/ehsuh/pggizs/zl92va8s0o59ibtn
doc_id: 284263053
exported_at: 2026-09-12T09:41:05
---

### <font style="color:rgb(15, 17, 21);">作用</font>
`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Autowired</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">告诉 Spring：“这个位置需要一个 Bean，你从容器里找一个类型匹配的，自动给我塞进去。”</font>

<font style="color:rgb(15, 17, 21);">它</font>**<font style="color:rgb(15, 17, 21);">自己不创建 Bean</font>**<font style="color:rgb(15, 17, 21);">，只是自动注入容器中已存在的 Bean。</font>

### <font style="color:rgb(15, 17, 21);">可以标注的位置</font>
**<font style="color:rgb(15, 17, 21);">1. 字段上（最常用）</font>**

```java
@RestController
public class OrderController {
    @Autowired
    private UserService userService;   // Spring 自动把 UserService 的 Bean 注入进来
}
```

**<font style="color:rgb(15, 17, 21);">2. 构造器上</font>**

```java
@RestController
public class OrderController {
    private final UserService userService;

    @Autowired
    public OrderController(UserService userService) {
        this.userService = userService;   // 构造器注入
    }
}
```

**<font style="color:rgb(15, 17, 21);">3. setter 方法上</font>**

```java
@RestController
public class OrderController {
    private UserService userService;

    @Autowired
    public void setUserService(UserService userService) {
        this.userService = userService;   // setter 注入
    }
}
```



### <font style="color:rgb(15, 17, 21);">工作原理（大白话）</font>
1. <font style="color:rgb(15, 17, 21);">Spring 启动时，会扫描所有标注了</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Component</font>`<font style="color:rgb(15, 17, 21);">（及</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Service</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Repository</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Controller</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">等）的类，创建它们的对象放入容器。</font>
2. <font style="color:rgb(15, 17, 21);">当 Spring 创建某个类时，如果发现里面某个字段/构造器/方法上有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Autowired</font>`<font style="color:rgb(15, 17, 21);">，它就去容器里找</font>**<font style="color:rgb(15, 17, 21);">类型匹配</font>**<font style="color:rgb(15, 17, 21);">的 Bean。</font>
3. <font style="color:rgb(15, 17, 21);">找到，就自动赋值；找不到，默认会报错（除非设置 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">required = false</font>`<font style="color:rgb(15, 17, 21);">）。</font>

### <font style="color:rgb(15, 17, 21);">注意</font>
+ <font style="color:rgb(15, 17, 21);">默认</font>**<font style="color:rgb(15, 17, 21);">按类型</font>**<font style="color:rgb(15, 17, 21);">查找。如果容器里有多个同类型的 Bean，会报错，需要配合</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Qualifier</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">指定名称（这个以后再说）。</font>
+ <font style="color:rgb(15, 17, 21);">目前你只需要掌握字段注入即可。</font>

