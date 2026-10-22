---
title: 九、参数与 URL（复习）
url: https://www.yuque.com/ehsuh/pggizs/akn3eogxi508pv1d
doc_id: 289230370
exported_at: 2026-10-22T23:47:32
---

### 1 三种参数注解
| 注解 | 值在哪 | 例子 |
| --- | --- | --- |
| `@RequestBody` | **请求体**（JSON） | `POST /user/add` |
| `@PathVariable` | **URL 路径里**（`{}` 占位） | `DELETE /user/delete/{id}` |
| `@RequestParam` | `**?**`** 后面**，或表单字段 | `GET /ai/chat?q=...` |


**判据不是"单个还是多个"，是"值在哪"**。 `**@PathVariable**`** 必须在路径里写 **`**{}**`（告诉 Spring 哪一段是变量）；`**@RequestParam**`** 不用写任何占位**（靠名字匹配）。

### 2 URL 的组成
```plain
http://localhost:8080/ai/chat?q=你好
└协议┘ └─主机─┘ └端口┘ └路径┘ └查询串┘
```

+ **路径** = 路由前缀（类上 `@RequestMapping`）+ 方法路径（`@GetMapping`）
+ **查询串**是客户端拼的，**不写在注解里**
+ **请求头**（不在 URL 里）= 元数据（认证、内容类型）← 类比"信封上的字"

### 3 `q == null || q.isBlank()` 里的 null 不能删
```plain
String q = null;
q.isBlank();   // 💥 NullPointerException
```

`isBlank()` 是**实例方法**，null 上调不了。能安全工作靠的是**短路求值**：前半为 true → 后面不执行。

**记住这个模式**：`a == null || a.xxx()` —— 前面的 null 判断永远别删。

