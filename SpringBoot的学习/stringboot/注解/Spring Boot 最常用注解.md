---
title: Spring Boot 最常用注解
url: https://www.yuque.com/ehsuh/pggizs/ib55z0io8qom3dt5
doc_id: 284226688
exported_at: 2026-09-12T09:41:09
---

### <font style="color:rgb(15, 17, 21);">1. </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RestController</font>`
+ <font style="color:rgb(15, 17, 21);">标记在</font>**<font style="color:rgb(15, 17, 21);">类</font>**<font style="color:rgb(15, 17, 21);">上</font>
+ <font style="color:rgb(15, 17, 21);">告诉 Spring：“我是一个控制器类，专门处理浏览器发来的请求，返回的数据直接作为响应体（JSON）返回给前端”</font>
+ <font style="color:rgb(15, 17, 21);">就像餐厅服务员：接单 → 上菜</font>

### <font style="color:rgb(15, 17, 21);">2.</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`
+ <font style="color:rgb(15, 17, 21);">标记在</font>**<font style="color:rgb(15, 17, 21);">类</font>**<font style="color:rgb(15, 17, 21);">或</font>**<font style="color:rgb(15, 17, 21);">方法</font>**<font style="color:rgb(15, 17, 21);">上</font>
+ <font style="color:rgb(15, 17, 21);">告诉 Spring：“这个类/方法处理哪个网址的请求”</font>
+ <font style="color:rgb(15, 17, 21);">类上写</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/user</font>`<font style="color:rgb(15, 17, 21);">，方法上写</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/login</font>`<font style="color:rgb(15, 17, 21);">，实际路径 =</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/user/login</font>`
+ <font style="color:rgb(15, 17, 21);">路径是</font>**<font style="color:rgb(15, 17, 21);">相对于服务器根路径</font>**<font style="color:rgb(15, 17, 21);">的</font>

```java
@RestController
@RequestMapping("/user")           // 类上的前缀
public class UserController {

    @RequestMapping("/login")     // 完整路径 = /user/login
    public String login() {
        return "登录成功";
    }

    @RequestMapping("")           // 完整路径 = /user（空字符串不追加）
    public String index() {
        return "用户模块首页";
    }
}
```



## <font style="color:rgb(15, 17, 21);">补充二：</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">详细说明</font>
### <font style="color:rgb(15, 17, 21);">类上的</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">是“前缀”，只对带有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">的方法生效</font>
<font style="color:rgb(15, 17, 21);">看代码：</font>

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/login")     // 完整路径 = /user/login
    public String login() {
        return "登录成功";
    }

    @RequestMapping("")           // 完整路径 = /user （空字符串，不追加）
    public String index() {
        return "用户模块首页";
    }

    // 没有 @RequestMapping，外部无法访问，类上的 /user 对它不起作用
    private boolean checkPassword(String password) {
        return password.length() >= 6;
    }
}
```

<font style="color:rgb(15, 17, 21);">解释：</font>

+ <font style="color:rgb(15, 17, 21);">类上的</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping("/user")</font>`<font style="color:rgb(15, 17, 21);"> </font>**<font style="color:rgb(15, 17, 21);">只影响</font>**<font style="color:rgb(15, 17, 21);">类中那些</font>**<font style="color:rgb(15, 17, 21);">自己也标注了</font>****<font style="color:rgb(15, 17, 21);"> </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>**`**<font style="color:rgb(15, 17, 21);"> </font>****<font style="color:rgb(15, 17, 21);">的方法</font>**<font style="color:rgb(15, 17, 21);">。</font>
+ <font style="color:rgb(15, 17, 21);">方法上的路径会拼接在类前缀后面：</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/user</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">+</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/login</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">=</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/user/login</font>`<font style="color:rgb(15, 17, 21);">。</font>
+ <font style="color:rgb(15, 17, 21);">方法上的</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping("")</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">表示不追加任何子路径，完整路径就是类前缀</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">/user</font>`<font style="color:rgb(15, 17, 21);">。</font>
+ **<font style="color:rgb(15, 17, 21);">没有 </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>**`**<font style="color:rgb(15, 17, 21);"> 的方法</font>**<font style="color:rgb(15, 17, 21);">完全不受类前缀影响，它根本不对外暴露，外面无法通过 URL 访问。它只是内部辅助方法。</font>

### <font style="color:rgb(15, 17, 21);">有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">vs 没有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`
| <font style="color:rgb(15, 17, 21);">类型</font> | <font style="color:rgb(15, 17, 21);">对外暴露 URL</font> | <font style="color:rgb(15, 17, 21);">示例</font> |
| --- | --- | --- |
| <font style="color:rgb(15, 17, 21);">有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>` | <font style="color:rgb(15, 17, 21);">暴露，浏览器可通过 URL 访问</font> | `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping("/login")</font>` |
| <font style="color:rgb(15, 17, 21);">没有</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>` | <font style="color:rgb(15, 17, 21);">不暴露，只能类内部调用</font> | `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">private boolean checkPassword(...)</font>` |


<font style="color:rgb(15, 17, 21);">所以类上的</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> </font><font style="color:rgb(15, 17, 21);">不是给整个类“贴路径”，而是给类中所有</font>**<font style="color:rgb(15, 17, 21);">标注了</font>****<font style="color:rgb(15, 17, 21);"> </font>**`**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>**`**<font style="color:rgb(15, 17, 21);"> </font>****<font style="color:rgb(15, 17, 21);">的方法</font>**<font style="color:rgb(15, 17, 21);">统一加前缀。</font>

---

## <font style="color:rgb(15, 17, 21);">总结</font>
+ `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Autowired</font>`<font style="color:rgb(15, 17, 21);">：自动注入 Bean，可标注字段、构造器、setter，默认按类型查找。</font>
+ `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);">：类上的作为路径前缀，只对带 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@RequestMapping</font>`<font style="color:rgb(15, 17, 21);"> 的方法生效；方法上的决定具体路径；没有该注解的方法不对外暴露。</font>





### <font style="color:rgb(15, 17, 21);">3. </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Autowired</font>`
+ <font style="color:rgb(15, 17, 21);">标记在</font>**<font style="color:rgb(15, 17, 21);">字段/构造器/方法</font>**<font style="color:rgb(15, 17, 21);">上</font>
+ <font style="color:rgb(15, 17, 21);">告诉 Spring：“我这个字段需要注入一个 Bean 对象，你从容器里找一个符合类型的给我，自动赋值”</font>
+ <font style="color:rgb(15, 17, 21);">它</font>**<font style="color:rgb(15, 17, 21);">不创建对象</font>**<font style="color:rgb(15, 17, 21);">，只是拿来用</font>

### <font style="color:rgb(15, 17, 21);">4.</font><font style="color:rgb(15, 17, 21);"> </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Component</font>`
+ <font style="color:rgb(15, 17, 21);">标记在</font>**<font style="color:rgb(15, 17, 21);">类</font>**<font style="color:rgb(15, 17, 21);">上</font>
+ <font style="color:rgb(15, 17, 21);">告诉 Spring：“我是一个普通的 Bean，请把我加入 Spring 容器管理”</font>
+ `<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Service</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Repository</font>`<font style="color:rgb(15, 17, 21);">、</font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Controller</font>`<font style="color:rgb(15, 17, 21);"> 内部都包含 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">@Component</font>`<font style="color:rgb(15, 17, 21);"> 的功能，只是语义更明确</font>

