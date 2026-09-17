---
title: 自定义注解 @interface
url: https://www.yuque.com/ehsuh/pggizs/oc500c82imlxwgux
doc_id: 284228501
exported_at: 2026-09-12T09:41:07
---

用 `@interface` 定义注解（注意不是 `interface`）：

```java
public @interface MyAnnotation {
    String value() default "默认值";
}
```

使用：

```java
@MyAnnotation(value = "你好")
public class MyClass {
}
```

**重要：自定义的注解本身没有任何功能，它只是一个标签。**  
除非你写代码去识别并处理它，否则它什么都不做。  
Spring 的注解之所以有用，是因为 Spring 内部有大量代码专门扫描和处理这些注解。

