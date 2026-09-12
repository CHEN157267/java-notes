---
title: HTTP 方法
url: https://www.yuque.com/ehsuh/pggizs/glgf0pm45ggo0l4n
doc_id: 284310884
exported_at: 2026-09-12T09:41:02
---

<font style="color:rgb(15, 17, 21);">HTTP 方法就是请求的“动作类型”，告诉后端“我发这个请求是想干什么”。</font>

| <font style="color:rgb(15, 17, 21);">HTTP 方法</font> | <font style="color:rgb(15, 17, 21);">动作</font> | <font style="color:rgb(15, 17, 21);">对应数据库操作</font> |
| --- | --- | --- |
| `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">GET</font>` | <font style="color:rgb(15, 17, 21);">获取数据（看）</font> | <font style="color:rgb(15, 17, 21);">查（SELECT）</font> |
| `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">POST</font>` | <font style="color:rgb(15, 17, 21);">提交数据（新增）</font> | <font style="color:rgb(15, 17, 21);">增（INSERT）</font> |
| `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">PUT</font>` | <font style="color:rgb(15, 17, 21);">更新数据（改）</font> | <font style="color:rgb(15, 17, 21);">改（UPDATE）</font> |
| `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">DELETE</font>` | <font style="color:rgb(15, 17, 21);">删除数据（删）</font> | <font style="color:rgb(15, 17, 21);">删（DELETE）</font> |


`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>**`**<font style="color:rgb(15, 17, 21);"> 默认不区分 HTTP 方法，所有请求都会匹配。</font>**<font style="color:rgb(15, 17, 21);">  
</font><font style="color:rgb(15, 17, 21);">Spring Boot 提供了更具体的注解：</font>

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

**<font style="color:rgb(15, 17, 21);">路径变量 </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">{id}</font>**`<font style="color:rgb(15, 17, 21);">：表示 URL 中这一部分是可变的，配合 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@PathVariable</font>`<font style="color:rgb(15, 17, 21);"> 获取值。</font>

```java
@GetMapping("/{id}")
public String getUser(@PathVariable("id") Long id) {
    return "查询用户，id 是：" + id;
}
```

