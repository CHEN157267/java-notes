---
title: 自定义注解 @interface
url: https://www.yuque.com/ehsuh/pggizs/oc500c82imlxwgux
doc_id: 284228501
exported_at: 2026-09-12T09:41:07
---

<font style="color:rgb(15, 17, 21);">用 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@interface</font>`<font style="color:rgb(15, 17, 21);"> 定义注解（注意不是 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">interface</font>`<font style="color:rgb(15, 17, 21);">）：</font>

```java
public @interface MyAnnotation {
    String value() default "默认值";
}
```

<font style="color:rgb(15, 17, 21);">使用：</font>

```java
@MyAnnotation(value = "你好")
public class MyClass {
}
```

**<font style="color:rgb(15, 17, 21);">重要：自定义的注解本身没有任何功能，它只是一个标签。</font>**  
<font style="color:rgb(15, 17, 21);">除非你写代码去识别并处理它，否则它什么都不做。</font>  
<font style="color:rgb(15, 17, 21);">Spring 的注解之所以有用，是因为 Spring 内部有大量代码专门扫描和处理这些注解。</font>

