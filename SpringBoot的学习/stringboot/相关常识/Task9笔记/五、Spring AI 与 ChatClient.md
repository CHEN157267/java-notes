---
title: 五、Spring AI 与 ChatClient
url: https://www.yuque.com/ehsuh/pggizs/luitg4t8zbtnpoqy
doc_id: 289218241
exported_at: 2026-10-22T23:47:29
---

### 1 Spring AI 是什么
**客户端库**：帮你把"发一句话给大模型"这件事包装好（拼 JSON、加认证头、发 HTTPS、解析响应）。

**它干的事**：

```plain
填地址（base-url）+ 填路径（/chat/completions）
+ 填认证头（Authorization: Bearer <key>）
+ 填请求体（{"model":"deepseek-chat","messages":[...]}
```

**类比**：`JdbcTemplate` 之于数据库 / `ChatClient` 之于大模型。

### 2 ChatClient 的类结构
```plain
ChatClient（接口）
├─ 实现类：DefaultChatClient
└─ 嵌套接口：Builder
      └─ 实现类：DefaultChatClientBuilder
```

+ `ChatClient` 和 `Builder` 是**两个独立接口**（Builder 只是"写在 ChatClient 内部"）
+ **容器里只有 **`**ChatClient.Builder**`** 这个 bean**（我解 `ChatClientAutoConfiguration` 确认过，没有 `ChatClient` 的 bean）

### 2.1 接口变量的三种来源（本项目三种都出现了）
| 接口 | 实现对象从哪来 | 例子 |
| --- | --- | --- |
| **Service** | **Spring 容器创建**（`@Service` 标在**实现类**上，不是接口） | `UserService` → `UserServiceImpl` |
| **Mapper** | **MyBatis 造好动态代理对象**，再**注册进 Spring**（Spring 只负责登记和发放，不负责造） | `UserMapper` |
| **ChatClient** | **我们自己在构造器里 **`**builder.build()**`** 造** | `AiServiceImpl` 的 `chatClient` 字段 |


**共同点**：都是"**接口变量 → 某个实现对象**"（多态）。 **区别**：**谁给你这个对象** —— 容器 / MyBatis / 你自己。

补充：Spring 默认是**单例** —— 同一个 bean 实例发给所有需要的地方（不是每次新建、也不是"池"）。 推论：**单例 bean 必须无状态/线程安全**，所以 Service 里不能存"每个请求不同的数据"。

### 3 方法链与类型变化
| 步骤 | 返回类型 |
| --- | --- |
| `.prompt()` | `ChatClientRequestSpec` |
| `.user(q)` | `ChatClientRequestSpec`（**还是它**） |
| `.call()` | `**CallResponseSpec**` ← 换对象、发请求、阻塞等待 |
| `.content()` | `**String**` ← 出链 |


**规律**：**中间步骤返回"下一步能用的接口"，最后一步返回"真正的值"**。 （跟 `Stream` 一样：`filter().map()` 还是 Stream，`collect()` 才出链成 List。）

**Fluent API 的意义**：**用类型引导调用顺序** —— 拿到 `RequestSpec` 你只能填 system/user/call，**不能**直接 `content()`。

### 4 为什么要注入 Builder，而不是直接给 ChatClient
**因为框架要留"定制口"**：

```plain
this.chatClient = builder
        .defaultSystem("你是一个简洁的助手")   // 预设人设
        .defaultOptions(...)                  // 预设参数
        .defaultAdvisors(...)                 // 预设拦截器
        .build();
```

**如果框架直接给你成品，这些就没法在构造时设置了。**

### 5 ⚠️ 枚举的真实作用（亲自验证过）
Spring AI 里有 `DeepSeekApi.ChatModel` 枚举，只有 `deepseek-chat` / `deepseek-reasoner`。

**它的作用只有两个，且都发生在"写 Java 代码"时**：

1. **IDE 自动补全**（你打 `DEEPSEEK_` 它列候选）
2. **编译器校验**（写错 → 找不到符号 → 编译不过）

**它不会"自动替换"，也不会"跳出来提醒"。**

**而且我们根本用不上它**：我们在 `application.properties` 里写的是**纯字符串**——

实测：把 properties 里的模型名删掉重敲，**IDE 没有任何提示**（连输入 `i` 都不会像 `int` 那样弹候选），只有 AI 补全工具会瞎猜。

**这就是"配置式"和"代码式"的区别**：

+ **代码式**：走枚举 → 有补全和校验
+ **配置式**：走字符串 → **没有任何保护，写错只能等运行时才知道**



