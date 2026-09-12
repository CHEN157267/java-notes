---
title: 真实项目中的 catch：不是只打印消息
url: https://www.yuque.com/ehsuh/oguki0/gth999duph982svs
doc_id: 284087343
exported_at: 2026-09-12T10:37:11
---

**<font style="color:rgb(15, 17, 21);">核心：catch 里要根据异常类型做不同的处理逻辑，不只是打印。</font>**

<font style="color:rgb(15, 17, 21);">例如用户注册功能：</font>

```java
try {
    register(user);
} catch (UsernameExistsException e) {
    return Result.fail("用户名已被占用");        // 返回业务错误
} catch (InvalidEmailException e) {
    return Result.fail("邮箱格式不正确");        // 返回业务错误
} catch (DataAccessException e) {
    logger.error("数据库异常", e);              // 记录严重日志
    sendAlertToDeveloper("数据库连接失败");     // 通知开发
    return Result.fail("系统繁忙，请稍后重试");  // 返回通用错误
}
```

**<font style="color:rgb(15, 17, 21);">为什么不能全用</font>****<font style="color:rgb(15, 17, 21);"> </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">Exception</font>**`**<font style="color:rgb(15, 17, 21);"> </font>****<font style="color:rgb(15, 17, 21);">+ 自定义消息？</font>**

+ <font style="color:rgb(15, 17, 21);">如果全用</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">Exception</font>`<font style="color:rgb(15, 17, 21);">，catch 里只能拿到一个</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">Exception</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">对象，无法用代码自动区分错误类型。</font>
+ <font style="color:rgb(15, 17, 21);">只能靠字符串匹配（如</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">if (e.getMessage().contains("用户名"))</font>`<font style="color:rgb(15, 17, 21);">），脆弱且不可靠。</font>
+ <font style="color:rgb(15, 17, 21);">不同异常类型需要触发不同动作：有的返回前端提示，有的发告警，有的记日志。</font>
+ <font style="color:rgb(15, 17, 21);">所以需要不同的异常子类，让 catch 能分类处理。</font>

**<font style="color:rgb(15, 17, 21);">同一时刻只会抛出一个异常</font>**<font style="color:rgb(15, 17, 21);">，不会同时出现多个异常。所以多个 catch 是为了覆盖不同位置可能出现的不同异常类型，不是担心同时出现多个。</font>

  
 

