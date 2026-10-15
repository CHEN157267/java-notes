---
title: 七、那个 favicon 事故
url: https://www.yuque.com/ehsuh/pggizs/pprfrezz8ukkfz4o
doc_id: 288322211
exported_at: 2026-10-15T19:53:00
---

### ① favicon 是什么
**favicon = favorites icon**（网站图标 / 站点图标）。浏览器打开任何网页，会**自动**向 `域名/favicon.ico` 要一张小图标，贴在**标签页 / 地址栏 / 收藏夹**上——**我们一个字没写，是浏览器自己要的**。

它**不是**"访问足迹"（那是 history）。一句话：**history = 我去过谁家；favicon = 那家门口的门牌。**

### ② 原来为什么变成 500
项目里没有这个静态资源 → Spring 抛〔原文引用〕：

```plain
org.springframework.web.servlet.resource.NoResourceFoundException: No static resource favicon.ico.
```

它是 `Exception` 的后代 → 被最宽的 `@ExceptionHandler(Exception.class)` 圈进去 → 吞成 500。

### ③ ★ 一个更狠的真相（本轮读源码挖到的）
〔原文引用：`NoResourceFoundException.java` + `DefaultHandlerExceptionResolver.java`〕

+ `NoResourceFoundException extends ServletException implements ErrorResponse`；
+ `DefaultHandlerExceptionResolver`（第 ③ 个 resolver）**本来就有 **`**handleNoResourceFoundException**`**，会把它转成 404**，而且 `logException` 对它**只打 DEBUG**（视为预期，不惊动）。

**那为什么我们当初是 500？** 因为第 ① 个 `ExceptionHandlerExceptionResolver` 里，**我们那个 **`**@ExceptionHandler(Exception.class)**`** 太宽，先一步把它抢走了** → 后面的 404 永远轮不到。

**这就是"兜底越宽，吞得越多"的现场物证** —— 我们亲手把一个本该 404 的请求，变成了 500。

### ④ 修好它 = 给一个更精确的 handler
`NoResourceFoundException` 比 `Exception`**更具体** → 按"最贴近"挑，优先落到我们新加的 handler，**兜底抢不走**。

### ⑤ `log.warn("资源未找到: {}", e.getMessage())` 里的 `{}`
**占位符**，运行时被后面的参数填进去（多个按顺序对应）。 **为什么不用 **`**+**`** 拼**：`+` 在调用 log **之前**就拼好了（参数求值阶段），**不管**日志级别够不够、会不会输出；而 `{}` 是 log **内部**判完级别、**真要输出了**才格式化。 → 术语叫 **惰性求值（lazy evaluation）**；日志调用一天几百万次，差别就出来了。

顺带解开一个疑点：**最后一个参数如果是异常对象、又没有对应的 **`**{}**`**，SLF4J 会把它当"异常"打印整条堆栈** —— 这正是 `log.warn("资源未找到", e)` 会刷屏的原因。

### ⑥ 为什么它不该算业务异常、也不该走兜底
+ **不是业务异常**：业务异常 = "用户能理解、能应对的业务结果"（重名、不存在）；favicon 跟"用户想干的事"无关。
+ **不该算系统异常 / 不该走兜底**：浏览器请求一个**根本不存在的地址**，是**客户端**问题（HTTP 层面就叫"资源未找到"），**不是服务端故障**。记成 500 + ERROR 日志 = **把常态当故障**，污染日志、误报监控。

---

