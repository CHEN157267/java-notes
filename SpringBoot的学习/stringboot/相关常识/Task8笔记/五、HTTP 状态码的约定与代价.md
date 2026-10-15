---
title: 五、HTTP 状态码的约定与代价
url: https://www.yuque.com/ehsuh/pggizs/hpup823cgsdgfilp
doc_id: 288319236
exported_at: 2026-10-15T19:52:59
---

### ① 为什么恒 200〔实测：成功/400/404/409/500 五种情况的 HTTP 全是 200〕
异常被 handler **接住**、handler **正常 **`**return**`** 了一个对象**（没继续往外抛）→ 对 Spring 来说"**这个请求处理成功了**" → 默认 200。 关键：**我们的 handler 方法没标 **`**@ResponseStatus**` → 用默认 200；语义全写进 body 的 `code`。

### ② 那"成功还是失败"放哪了
放在 `**Result.code**` 里（200/400/404/409/500 都是 body 里的数字）。

### ③ 外部调用方的隐患（真实项目最大争议点）
前端 / 网关 / 监控**默认按 HTTP 状态码判成败**：

| 谁 | 假 200 会出什么事 |
| --- | --- |
| 前端 axios 拦截器 | 只在**非 2xx** 时进 `catch`；永远 200 → **失败也走 **`**then**`** 成功分支**，业务方得自己再判 code，一忘就出错 |
| 监控 / 告警 | 只统计 5xx 当故障 → **500 被算成"正常请求"**，不报警 |
| 重试 / 熔断 / 限流 | 按状态码决定 → 对"假 200"完全不生效 |
| CDN / 缓存 / 网关 | 可能把"200"当成功结果**缓存**，错误也被缓存 |


**一句话**：**HTTP 状态是给基础设施看的，body.code 是给业务看的**。HTTP 200 是"服务端一切正常"的对外承诺，别让 body.code 借它撒谎。 

### ④ 「两处判、容易漏」是什么意思
失败信号被拆进**两条通道**（HTTP 码 + body.code），消费者**两条都得查**，于是前端要写**两段几乎一样的错误处理**：

```plain
axios.put('/user/update', d)
  .then(res => { if (res.data.code !== 200) showError(res.data.msg); }) // 管 body.code
  .catch(err => { showError(err.response.data.msg); });                 // 管 HTTP 码
```

统一成 **200 + body.code**，就把它**压回一处**。

补充答一个常见误区：**非 2xx 时响应体照样会到前端**，只是 axios 默认丢进 `catch`，body 在 `error.response.data` 里能取到。所以不是"收不到数据"，是"**走的是失败分支**"。

### ⑤ `@ResponseStatus` 是干嘛的（范围比想象的大）
〔原文引用：`spring-web-6.2.19``ResponseStatus.java`〕

`Marks a method or exception class with the status ... that should be returned.`

能贴**三种地方**：① 异常类上 ② handler 方法上（含 `@ExceptionHandler`） ③ 控制器类上（子类继承）。 所以它是个通用的"**这条响应用哪个 HTTP 状态码**"工具——新建成功回 201、删除成功回 204，也靠它，**不限**于异常。

**同一份文件的官方警告**〔原文引用〕：

贴在**异常类**上、或设了 `reason` → 会走 `HttpServletResponse.sendError` → 容器丢一张 **HTML 错误页**，"**unsuitable for REST APIs**"。

我们没踩：贴的是**方法**、也没写 `reason`，只设状态码。

### ⑥ 我们实际用到的地方〔实测〕
favicon 的 handler 加了 `@ResponseStatus(HttpStatus.NOT_FOUND)`，实测 **HTTP 状态真的变成 404**（此前是 200 + body.code 404）。

**代价**：这让 favicon 成了我们项目里**唯一"真 404"的接口**，破了"HTTP 恒 200"的约定。但对**静态资源**这是对的——它本来就不是我们的 API。主体仍保持 200 + body.code。

### ⑦ "业务码 → HTTP 码要统一映射"指什么
不是单个 handler 里两个数字对齐那么简单，而是**全项目要一套一致规则**，例如：

| body.code | HTTP 码 | 场景 |
| --- | --- | --- |
| 400 | 400 | 参数不合法 |
| 404 | 404 | 资源不存在 |
| 409 | 409 | 冲突（重名） |


**一旦不全用**（我们就是），就出现"有的错走 HTTP 语义、有的错埋在 body 里"——对消费者就是"要么两处判、要么摸不清规律"，这就是"乱"。

