---
title: 四、异常怎么找到 handler ★
url: https://www.yuque.com/ehsuh/pggizs/gmq9pkyh0w3gsoel
doc_id: 288124868
exported_at: 2026-10-15T19:52:58
---

### 真实链路（6.2.19 源码级）
```plain
Service 抛异常
   ↓ 冒泡（Controller 只是"路过"，不是角色）
① DispatcherServlet              ← 执行 handler 的地方，本身就有一层 catch(Throwable)
   ↓ 把异常交给 resolver 列表，按顺序挨个试
② List<HandlerExceptionResolver> ← 装着"实现类实例"的有序列表
   ↓ 试到 ExceptionHandlerExceptionResolver（第一个能处理的）
③ ExceptionHandlerExceptionResolver ← 真正去 @ControllerAdvice 里找 @ExceptionHandler
   ↓ 按"最具体"挑出
④ 我们的 handler 方法              ← 最终 return Result
```

### 关键机制：不是"挑"，是"挨个试"
〔原文引用：`spring-webmvc-6.2.19``DispatcherServlet.processHandlerException`〕

```plain
for (HandlerExceptionResolver resolver : this.handlerExceptionResolvers) {
    exMv = resolver.resolveException(request, response, handler, ex);
    if (exMv != null) { break; }   // 第一个接住的赢，立刻停
}
```

原文引用：`initHandlerExceptionResolvers`〕列表由 `AnnotationAwareOrderComparator.sort(...)` 排序。

**所以：不存在"先挑接口、再挑实现类"的两层匹配**。就是一个**有序的实现类实例列表**，挨个调用 `resolveException(...)`，**谁先返回非 null 谁赢**。

### 默认的三个实现〔原文引用：`DispatcherServlet.properties`〕
| 顺序 | 实现类 | 干什么 |
| --- | --- | --- |
| 1 | `ExceptionHandlerExceptionResolver` | 读我们的 `@ExceptionHandler`（**我们的兜底就在这层**） |
| 2 | `ResponseStatusExceptionResolver` | 读**异常类上**的 `@ResponseStatus` → 转 HTTP 码 |
| 3 | `DefaultHandlerExceptionResolver` | Spring 内置异常 → 对应 HTTP 码（405/415/404…） |


### handler 怎么挑：按类型，且「最具体」优先
`ExceptionDepthComparator`：谁离抛出的异常在**继承树上更近**，用谁。

+ `BusinessException` → 落到 `handleBusinessException`（它比 `Exception` 更具体，**兜底抢不走**）。
+ `NullPointerException` → 落 `Exception` 兜底 → 500。

### ⚠️ 本次自测踩的坑
+ Q4.1 只答了 `service → controller → advice`，**漏了 **`**DispatcherServlet**`** 和两个 Resolver**。
+ 复述时**两次**把机制说成"先挑接口再挑实现类"。正确说法 = **DispatcherServlet 拿着有序列表挨个试**。

