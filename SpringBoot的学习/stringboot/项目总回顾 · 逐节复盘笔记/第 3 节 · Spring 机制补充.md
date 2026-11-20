---
title: 第 3 节 · Spring 机制补充
url: https://www.yuque.com/ehsuh/pggizs/sxad5nkkxa3mvx09
doc_id: 292632716
exported_at: 2026-11-20T09:59:30
---

### 3.1 `@RestControllerAdvice` 是怎么被认出来的
```plain
@RestControllerAdvice
  = @ControllerAdvice + @ResponseBody
        ↓
  @ControllerAdvice 的元注解链上有 @Component
        ↓
  能被组件扫描扫到，成为一个 bean
```

**Spring 的扩展点大多靠注解，不靠继承。** 对比 Servlet 时代必须 `extends HttpServlet` —— Spring 把这条路换成了“贴个注解，有人来扫”。

那个“人”叫 `ExceptionHandlerExceptionResolver`，它在**启动时**做三件事：

1. 找出所有带 `@ControllerAdvice` 的 bean；
2. 扫它们方法上的 `@ExceptionHandler`；
3. 给**每个 advice 各建一张**「异常类型 → 处理方法」的表。

### 3.2 多个 advice 时，谁生效
**不是一张全局大表，是“每个 advice 一张表 + 一个适用性检查”。**

```plain
异常发生
  ↓
Resolver 按顺序遍历 advice 列表
  ↓
对每个 advice 先问：它适用于当前 controller 吗？（isApplicableToBeanType）
  ↓ 适用
在【它自己那张表】里按异常类型查 → 命中就调用，结束
```

**为什么只能遍历**：advice 的适用范围是“条件”（`basePackages` / `assignableTypes` / `annotations`），**没有反向索引**能从 controller 直接跳到匹配的 advice，所以只能逐个判断。

**遍历顺序由 **`**@Order**`** 或 **`**Ordered**`** 接口决定**（数字小的先），不是随机的。**多个 advice 都匹配同一异常时，先到的赢，后面的不执行。**

### 3.3 `@Bean` 的真正作用：保证“只有一个”
**不是“帮 Spring 创建对象”，而是“保证全场共享同一个实例”。**

判断标准：**这个对象有没有状态？**

| 类型 | 有状态？ | 到处 new 行不行 | 例子 |
| --- | --- | --- | --- |
| 工具类、配置好的客户端 | ❌ | ✅ 无所谓 | `ChatClient`、`ObjectMapper` |
| 缓存、向量库、连接池 | ✅ | ❌ **数据会分家** | `SimpleVectorStore`、`DataSource` |


**反例演示**（如果不用 `@Bean`，各在构造器里 build）：

```plain
RagLoader       → build 出 A，往里存 138 个块
RagServiceImpl  → build 出 B，去 B 里查 → 空的 → 永远查不到
```

`**SimpleVectorStore**`** 必须用 **`**@Bean**`** 的三个叠加原因**：

1. 类上没有 `@Component` → 不在扫描范围；
2. 构造器是 `protected` → Spring 常规流程调不到；
3. 需要一个 `EmbeddingModel` 参数 → 官方让你用 `builder()` 组装。

### 3.4 `@Valid` 管不了 `@RequestParam`
| 目标 | 该怎么校验 |
| --- | --- |
| `@RequestBody` 里**对象的字段** | `@Valid` + `@NotBlank` 等 |
| `@RequestParam` 的**单个参数** | `@Valid`**无效** |


`@RequestParam` 想校验，两条路：

```plain
// 路一：手动判（简单，本项目采用）
if (q == null || q.isBlank()) {
    log.warn("q 为空，已拒绝");
    return Result.error(400, "q 不能为空");
}
```

```plain
// 路二：注解式（类上必须有 @Validated，且要额外处理 ConstraintViolationException）
@Validated
public class RagController {
    public Result<...> search(@RequestParam @NotBlank String q, ...)
}
```

**路二的两个成本**：类上加 `@Validated`（Spring 的，不是 `@Valid`）；抛出的 `ConstraintViolationException` 要另加 handler。**学习项目走路一就够。**

### 3.5 HTTP 状态码 vs 业务码
本项目所有 handler 返回的 `Result`，**HTTP 状态码都是 200**，业务码在 body 的 `code` 字段里（400/503/500）。唯一例外是 `handleNoResourceFoundException`，加了 `@ResponseStatus(NOT_FOUND)`。

| 风格 | 前端怎么看 | 谁在用 |
| --- | --- | --- |
| HTTP 200 + body 带业务码 | 只看 `code` | 国内大量项目 |
| HTTP 状态码与业务码一致 | 看 HTTP 状态 | RESTful 派 |


**不是 bug，是约定选择。** 本项目选第一种，知道这个事实就行。

### 3.6 `Path.of` 的相对路径从哪算
从 **JVM 的工作目录**（working directory）算，**不是项目根目录**：

| 运行方式 | 工作目录 |
| --- | --- |
| IDEA 里跑 | 模块根目录（`demo/`） |
| `java -jar` | 你敲命令时所在的目录 |
| 双击 jar | 视系统而定 |


**所以配置里推荐 **`**classpath:**`** 而不是相对路径** —— `classpath:` 跟着 class 文件走，打成 jar 也有效；相对路径会随“从哪启动”而变。

