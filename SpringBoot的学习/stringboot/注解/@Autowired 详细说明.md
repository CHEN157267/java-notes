---
title: @Autowired 详细说明
url: https://www.yuque.com/ehsuh/pggizs/zl92va8s0o59ibtn
doc_id: 284263053
exported_at: 2026-09-12T09:41:05
---

### 作用
`@Autowired` 告诉 Spring：“这个位置需要一个 Bean，你从容器里找一个类型匹配的，自动给我塞进去。”

它**自己不创建 Bean**，只是自动注入容器中已存在的 Bean。

### 可以标注的位置
**1. 字段上（最常用）**

```java
@RestController
public class OrderController {
    @Autowired
    private UserService userService;   // Spring 自动把 UserService 的 Bean 注入进来
}
```

**2. 构造器上**

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

**3. setter 方法上**

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



### 工作原理（大白话）
1. Spring 启动时，会扫描所有标注了 `@Component`（及 `@Service`、`@Repository`、`@Controller` 等）的类，创建它们的对象放入容器。
2. 当 Spring 创建某个类时，如果发现里面某个字段/构造器/方法上有 `@Autowired`，它就去容器里找**类型匹配**的 Bean。
3. 找到，就自动赋值；找不到，默认会报错（除非设置 `required = false`）。

### 注意
+ 默认**按类型**查找。如果容器里有多个同类型的 Bean，会报错，需要配合 `@Qualifier` 指定名称（这个以后再说）。
+ 目前你只需要掌握字段注入即可。

