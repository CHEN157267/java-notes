---
title: 常用的Exception方法
url: https://www.yuque.com/ehsuh/oguki0/kxvagmi804uvqygl
doc_id: 284080030
exported_at: 2026-09-12T10:37:13
---

## `getMessage()`
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

## `printStackTrace()`
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





#### `e.getMessage()`
+ 返回异常消息的**字符串**（如 `"/ by zero"`）。
+ 需要自己用 `System.out.println` 或 `System.err.println` 打印。

#### `e.printStackTrace()`
+ **直接打印完整异常堆栈**，包括异常类型、消息、调用链（类名、方法名、行号）。
+ 不需要额外用 `sout` 包，默认输出到 `System.err`（错误流），显示在控制台。
+ **两者都在控制台显示。** 区别：
+ `getMessage()` 返回字符串，灵活，可以存变量、写文件、发日志系统。
+ `printStackTrace()` 直接打印，信息详细，但没法拿到字符串做其他处理。

**为什么真实项目不全用**** **`**printStackTrace()**`**？**

+ 它只能打印到控制台，没法灵活地写入文件、数据库或日志平台。
+ 真实项目用日志框架（如 Logback、Log4j），通常配合 `log.error("消息", e)` 使用，既记录消息又记录堆栈。

**不需要背异常子类**，用 `catch (Exception e)` 就能接住绝大多数异常。等遇到具体需求再细分。

  
 

