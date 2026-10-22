---
title: 三、配置体系：application里的properties与pom里的properties标签
url: https://www.yuque.com/ehsuh/pggizs/vtkzxxotbluopryw
doc_id: 289216674
exported_at: 2026-10-22T23:47:28
---

| | pom 的 `<properties>` | `application.properties` |
| --- | --- | --- |
| 谁读 | **Maven**（构建工具） | **Spring Boot**（应用） |
| 何时生效 | **编译 / 打包时** | **启动时** |
| 作用 | 依赖版本、编译目标 | 连哪个库、端口、密钥、开关 |
| 打不打进 jar | **不**（用完即弃） | **会**（打进 jar，启动才读） |


### 1 四个配置来源的优先级（高 → 低）
```plain
① 命令行参数        --server.port=8080
② 环境变量          SERVER__PORT=63917
③ application.properties   server.port=xxx
④ 框架默认值        8080
```

**取值规则**：Spring 启动时把四个来源排成有序列表，**从上往下找，找到就用**。

**两个真实用例**：

+ **为什么要加 **`**--server.port=8080**`：本机有环境变量 `SERVER__PORT=63917`（双下划线会被解析成 `server.port`），它的优先级高于 properties，**只有命令行参数能压住它**
+ **为什么 **`**SERVER__PORT**`** 能生效**：环境变量名里的 `_` 会被 Spring 转换成 `.`（relaxed binding）

### 4.2 `${}` 什么时候被解析
**启动时**（不是"用到时"）。所以：

| 情况 | 结果 |
| --- | --- |
| properties 里**压根没写**`api-key` | **启动失败**：`DeepSeek API key must be set` |
| properties **写了**`${DEEPSEEK_API_KEY}`，但**环境变量缺失** | **能启动**（字面量被当 key、非空过关），**调用时才 401** |


⚠️ **这是 Task9 最阴险的坑**：第二种情况启动毫无报错，你会以为是代码问题。

