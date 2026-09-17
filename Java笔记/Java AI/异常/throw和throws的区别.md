---
title: throw和throws的区别
url: https://www.yuque.com/ehsuh/oguki0/isf0tlum1zdzwdki
doc_id: 284080269
exported_at: 2026-09-12T10:37:12
---

#### `throw`：主动抛出异常对象
+ 写在**方法体内部**，任何花括号内都可以，不一定要在 try 里。
+ 后面跟的是**异常对象**（`new XxxException(...)`）。
+ 执行到 throw 时，方法立刻中断，后面的代码不执行。
+ 异常会沿着调用栈向上传递，如果没有人 catch，程序终止并打印堆栈。

```java
public static int divide(int a, int b) {
    if (b == 0) {
        throw new ArithmeticException("除数不能为0");
    }
    return a / b;
}
```







#### `throws`：声明可能抛出的异常，自己不处理
+ 写在**方法签名末尾**（形参列表之后，方法体之前）。
+ 后面跟的是**异常类名**（不是对象，不能写 `new`）。
+ 表示“我可能抛这个异常，谁调用我谁处理”。

```java
public static int divide(int a, int b) throws ArithmeticException {
    return a / b;   // 可能抛异常，但不处理，甩给调用者
}
```

调用者处理：

```java
try {
    divide(10, 0);
} catch (ArithmeticException e) {
    System.out.println("处理了异常：" + e.getMessage());
}
```

**对比：**

| | throw | throws |
| --- | --- | --- |
| 本质 | 动作：真的抛出异常对象 | 声明：告诉别人可能抛异常 |
| 位置 | 方法体内部 | 方法签名末尾 |
| 后面跟什么 | 异常对象（`new XxxException()`<br/>） | 异常类名（`XxxException`<br/>） |
| 谁处理 | 由上层 catch 接住 | 由调用者决定 catch 或继续 throws |


  
 

