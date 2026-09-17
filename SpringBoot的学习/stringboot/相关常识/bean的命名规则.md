---
title: bean的命名规则
url: https://www.yuque.com/ehsuh/pggizs/pbui1r0grka5cpa9
doc_id: 285544082
exported_at: 2026-09-17T22:25:37
---

**<font style="color:rgba(0, 0, 0, 0.9);">Spring 明文规定：实现类的对象的名字，是实现类的名字的首字母小写版。</font>**

```java
@Service
public class UserServiceImpl implements UserService { }
//        ↓ Spring 自动给它起名
//     bean 名 = "userServiceImpl"      ← 类名首字母小写

@Qualifier("userServiceImpl")           // ← 所以这里要写这个名字

```

规则细分：

<font style="color:rgba(0, 0, 0, 0.9);">准确叫法是 </font>**<font style="color:rgba(0, 0, 0, 0.9);">JavaBeans 的 </font>**`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">decapitalize</font>**`**<font style="color:rgba(0, 0, 0, 0.9);">（首字母小写化）</font>**

| **<font style="color:rgba(0, 0, 0, 0.9);">类名</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">bean 名</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">说明</font>** |
| --- | --- | --- |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">userServiceImpl</font>` | <font style="color:rgba(0, 0, 0, 0.9);">常规：首字母变小写</font> |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">URLService</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">URLService</font>` | **<font style="color:rgba(0, 0, 0, 0.9);">前两个字母都是大写 → 原样不动</font>** |
| `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UUserService</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UUserService</font>` | <font style="color:rgba(0, 0, 0, 0.9);">同上</font> |


<font style="color:rgba(0, 0, 0, 0.9);">为什么有特例？怕你写个 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">URLService</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 被变成 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">uRLService</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 太难看，所以约定"前两个字母都大写就不动"。</font>

<font style="color:rgba(0, 0, 0, 0.9);"></font>

<font style="color:rgba(0, 0, 0, 0.9);"></font>

<font style="color:rgba(0, 0, 0, 0.9);">手动给bean命名</font>

+ <font style="color:rgba(0, 0, 0, 0.9);">想自己起名，就写 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Service("userSvc")</font>`<font style="color:rgba(0, 0, 0, 0.9);"> → bean 名变成 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">userSvc</font>`<font style="color:rgba(0, 0, 0, 0.9);">，那 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Qualifier</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 也得跟着写 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">"userSvc"</font>`<font style="color:rgba(0, 0, 0, 0.9);">。</font>

