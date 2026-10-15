---
title: 三、throw / throws / checked 与 unchecked ★
url: https://www.yuque.com/ehsuh/pggizs/igybpd4mxktpvop7
doc_id: 288124658
exported_at: 2026-10-15T19:52:57
---

分工:

| 你的意图 | 写什么 |
| --- | --- |
| 我**要主动扔**一个异常出去 | `throw` |
| 我**不想管**，让它往上走 | `throws`（**只有 checked 才必须写**） |
| 我**就地解决**，不让它出去 | `try-catch` |


**谁有情绪谁 **`**throw**`**，谁不想管谁 **`**throws**`**，谁就地解决谁 **`**try-catch**`**。**

****

**为什么 Service 里 **`**throw new BusinessException(...)**`**，签名上一个 **`**throws**`** 都没有？**

** 因为 **`**BusinessException**`** 是 unchecked（**`**RuntimeException**`** 家族），编译器不管，不用声明。**

****

**什么时候必须写 **`**throws**`

** 声明一个 checked 异常（**`**Exception**`** 的子类，且不属于**`**RuntimeException**`** 家族）时——如 **`**IOException**`**。**

****

**异常的「三类来源」**

| **来源** | **例子** |
| --- | --- |
| **你的代码 **`**throw**` | `**throw new BusinessException("...", 409)**` |
| **JVM 运行时抛** | `**NullPointerException**`**、**`**ArrayIndexOutOfBoundsException**`**、**`**ArithmeticException**`**（除零）** |
| **框架/库抛** | `**NoResourceFoundException**`**（找不到静态资源）、**`**MethodArgumentNotValidException**`**（校验失败）、**`**HttpMessageNotReadableException**`**（JSON 坏格式）** |


**所以"没写异常代码就不会有异常"是错的 —— 后两类你一个字没写，照样会炸。**

****

+ **抛的动作永远发生在某个 **`**throw**`** 语句里****（或 JVM 抛）；****调用者可能只是"被路过"****——异常是他调的方法抛的，冒泡从他这穿过去，他要么 catch、要么放行（checked 才要挂 **`**throws**`**），****一个 **`**throw**`** 都不用写****。**
+ **只有当"想扔"的意图在他自己身上时，他才写 **`**throw**`**。**

