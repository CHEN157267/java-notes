---
title: throw和throws的区别
url: https://www.yuque.com/ehsuh/oguki0/isf0tlum1zdzwdki
doc_id: 284080269
exported_at: 2026-09-12T10:37:12
---

#### `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">throw</font>`<font style="color:rgb(15, 17, 21);">：主动抛出异常对象</font>
+ <font style="color:rgb(15, 17, 21);">写在</font>**<font style="color:rgb(15, 17, 21);">方法体内部</font>**<font style="color:rgb(15, 17, 21);">，任何花括号内都可以，不一定要在 try 里。</font>
+ <font style="color:rgb(15, 17, 21);">后面跟的是</font>**<font style="color:rgb(15, 17, 21);">异常对象</font>**<font style="color:rgb(15, 17, 21);">（</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">new XxxException(...)</font>`<font style="color:rgb(15, 17, 21);">）。</font>
+ <font style="color:rgb(15, 17, 21);">执行到 throw 时，方法立刻中断，后面的代码不执行。</font>
+ <font style="color:rgb(15, 17, 21);">异常会沿着调用栈向上传递，如果没有人 catch，程序终止并打印堆栈。</font>

```java
public static int divide(int a, int b) {
    if (b == 0) {
        throw new ArithmeticException("除数不能为0");
    }
    return a / b;
}
```



<font style="color:rgb(15, 17, 21);"></font>

<font style="color:rgb(15, 17, 21);"></font>

#### `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">throws</font>`<font style="color:rgb(15, 17, 21);">：声明可能抛出的异常，自己不处理</font>
+ <font style="color:rgb(15, 17, 21);">写在</font>**<font style="color:rgb(15, 17, 21);">方法签名末尾</font>**<font style="color:rgb(15, 17, 21);">（形参列表之后，方法体之前）。</font>
+ <font style="color:rgb(15, 17, 21);">后面跟的是</font>**<font style="color:rgb(15, 17, 21);">异常类名</font>**<font style="color:rgb(15, 17, 21);">（不是对象，不能写</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">new</font>`<font style="color:rgb(15, 17, 21);">）。</font>
+ <font style="color:rgb(15, 17, 21);">表示“我可能抛这个异常，谁调用我谁处理”。</font>

```java
public static int divide(int a, int b) throws ArithmeticException {
    return a / b;   // 可能抛异常，但不处理，甩给调用者
}
```

<font style="color:rgb(15, 17, 21);">调用者处理：</font>

```java
try {
    divide(10, 0);
} catch (ArithmeticException e) {
    System.out.println("处理了异常：" + e.getMessage());
}
```

**<font style="color:rgb(15, 17, 21);">对比：</font>**

| | <font style="color:rgb(15, 17, 21);">throw</font> | <font style="color:rgb(15, 17, 21);">throws</font> |
| --- | --- | --- |
| <font style="color:rgb(15, 17, 21);">本质</font> | <font style="color:rgb(15, 17, 21);">动作：真的抛出异常对象</font> | <font style="color:rgb(15, 17, 21);">声明：告诉别人可能抛异常</font> |
| <font style="color:rgb(15, 17, 21);">位置</font> | <font style="color:rgb(15, 17, 21);">方法体内部</font> | <font style="color:rgb(15, 17, 21);">方法签名末尾</font> |
| <font style="color:rgb(15, 17, 21);">后面跟什么</font> | <font style="color:rgb(15, 17, 21);">异常对象（</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">new XxxException()</font>`<br/><font style="color:rgb(15, 17, 21);">）</font> | <font style="color:rgb(15, 17, 21);">异常类名（</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">XxxException</font>`<br/><font style="color:rgb(15, 17, 21);">）</font> |
| <font style="color:rgb(15, 17, 21);">谁处理</font> | <font style="color:rgb(15, 17, 21);">由上层 catch 接住</font> | <font style="color:rgb(15, 17, 21);">由调用者决定 catch 或继续 throws</font> |


  
 

