---
title: 常用的Exception方法
url: https://www.yuque.com/ehsuh/oguki0/kxvagmi804uvqygl
doc_id: 284080030
exported_at: 2026-09-12T10:02:10
---

## `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">getMessage()</font>`
```java
public class ExceptionDemo1 {
    public static void main(String[] args) {
        System.out.println("程序开始");

        try {
            // 可能出错的代码
            int result = 10 / 0;   // 这里会抛出 ArithmeticException
            System.out.println("这行不会执行，因为上面已经出错");
        } catch (Exception e) {
            // 出错后跳到这里：接住异常，处理
            System.out.println("出错了，错误信息：" + e.getMessage());
        } finally {
            // 无论是否有异常，都会执行
            System.out.println("finally 执行，比如释放资源");
        }

        System.out.println("程序结束");
    }
}
```

## `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">printStackTrace()</font>`
```java
public static int divide(int a, int b) {
    try {
        return a / b;       // 1. 执行 a/b，b=0 会报错，所以这行 return 不会执行
    } catch (ArithmeticException e) {
        System.err.println("【错误】除法分母为0");  // 2. 执行
        e.printStackTrace();                       // 3. 执行
        return 0;                                  // 4. 执行，返回0
    }
}
```





#### `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">e.getMessage()</font>`
+ <font style="color:rgb(15, 17, 21);">返回异常消息的</font>**<font style="color:rgb(15, 17, 21);">字符串</font>**<font style="color:rgb(15, 17, 21);">（如</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">"/ by zero"</font>`<font style="color:rgb(15, 17, 21);">）。</font>
+ <font style="color:rgb(15, 17, 21);">需要自己用</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">System.out.println</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">或</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">System.err.println</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">打印。</font>

#### `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">e.printStackTrace()</font>`
+ **<font style="color:rgb(15, 17, 21);">直接打印完整异常堆栈</font>**<font style="color:rgb(15, 17, 21);">，包括异常类型、消息、调用链（类名、方法名、行号）。</font>
+ <font style="color:rgb(15, 17, 21);">不需要额外用 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">sout</font>`<font style="color:rgb(15, 17, 21);"> 包，默认输出到 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">System.err</font>`<font style="color:rgb(15, 17, 21);">（错误流），显示在控制台。</font>
+ **<font style="color:rgb(15, 17, 21);">两者都在控制台显示。</font>**<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">区别：</font>
+ `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">getMessage()</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">返回字符串，灵活，可以存变量、写文件、发日志系统。</font>
+ `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">printStackTrace()</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">直接打印，信息详细，但没法拿到字符串做其他处理。</font>

**<font style="color:rgb(15, 17, 21);">为什么真实项目不全用</font>****<font style="color:rgb(15, 17, 21);"> </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">printStackTrace()</font>**`**<font style="color:rgb(15, 17, 21);">？</font>**

+ <font style="color:rgb(15, 17, 21);">它只能打印到控制台，没法灵活地写入文件、数据库或日志平台。</font>
+ <font style="color:rgb(15, 17, 21);">真实项目用日志框架（如 Logback、Log4j），通常配合</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">log.error("消息", e)</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">使用，既记录消息又记录堆栈。</font>

**<font style="color:rgb(15, 17, 21);">不需要背异常子类</font>**<font style="color:rgb(15, 17, 21);">，用</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">catch (Exception e)</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">就能接住绝大多数异常。等遇到具体需求再细分。</font>

<font style="color:rgb(15, 17, 21);">  
</font><font style="color:rgb(15, 17, 21);"> </font>

