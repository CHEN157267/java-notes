---
title: HTTP 方法
url: https://www.yuque.com/ehsuh/pggizs/glgf0pm45ggo0l4n
doc_id: 284310884
exported_at: 2026-09-12T09:41:02
---

HTTP 方法就是请求的“动作类型”，告诉后端“我发这个请求是想干什么”。

| HTTP 方法 | 动作 | 对应数据库操作 |
| --- | --- | --- |
| `GET` | 获取数据（看） | 查（SELECT） |
| `POST` | 提交数据（新增） | 增（INSERT） |
| `PUT` | 更新数据（改） | 改（UPDATE） |
| `DELETE` | 删除数据（删） | 删（DELETE） |


`**@RequestMapping**`** 默认不区分 HTTP 方法，所有请求都会匹配。**  
Spring Boot 提供了更具体的注解：

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping("/{id}")        // 处理 GET /user/1
    public String getUser() {
        return "查询用户";
    }

    @PostMapping("")            // 处理 POST /user
    public String createUser() {
        return "新增用户";
    }

    @PutMapping("/{id}")        // 处理 PUT /user/1
    public String updateUser() {
        return "更新用户";
    }

    @DeleteMapping("/{id}")     // 处理 DELETE /user/1
    public String deleteUser() {
        return "删除用户";
    }
}
```

**路径变量 **`**{id}**`：表示 URL 中这一部分是可变的，配合 `@PathVariable` 获取值。

```java
@GetMapping("/{id}")
public String getUser(@PathVariable("id") Long id) {
    return "查询用户，id 是：" + id;
}
```

