---
title: 注入里的"依赖"与pom.xml 里的"依赖"的区别
url: https://www.yuque.com/ehsuh/pggizs/oy1523le2do6n8i9
doc_id: 285484406
exported_at: 2026-09-17T22:25:40
---

| **<font style="color:rgba(0, 0, 0, 0.9);">   </font>****<font style="color:rgba(0, 0, 0, 0.9);">pom.xml 里的"依赖"</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">注入里的"依赖"</font>** | |
| --- | --- | --- |
| <font style="color:rgba(0, 0, 0, 0.9);">指的是</font> | **<font style="color:rgba(0, 0, 0, 0.9);">库/jar 包</font>** | **<font style="color:rgba(0, 0, 0, 0.9);">一个对象</font>** |
| <font style="color:rgba(0, 0, 0, 0.9);">层面</font> | <font style="color:rgba(0, 0, 0, 0.9);">编译期的</font>**<font style="color:rgba(0, 0, 0, 0.9);">代码库</font>** | <font style="color:rgba(0, 0, 0, 0.9);">运行期的</font>**<font style="color:rgba(0, 0, 0, 0.9);">对象</font>** |
| <font style="color:rgba(0, 0, 0, 0.9);">例子</font> | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">spring-boot-starter-web</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);">、</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">mybatis-plus</font>` | `<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">需要的</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserMapper</font>`<br/><font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">对象</font> |
| <font style="color:rgba(0, 0, 0, 0.9);">你需要它的原因</font> | <font style="color:rgba(0, 0, 0, 0.9);">我的</font>**<font style="color:rgba(0, 0, 0, 0.9);">代码</font>**<font style="color:rgba(0, 0, 0, 0.9);">要用别人的类</font> | <font style="color:rgba(0, 0, 0, 0.9);">我的</font>**<font style="color:rgba(0, 0, 0, 0.9);">对象</font>**<font style="color:rgba(0, 0, 0, 0.9);">要另一个对象才能干活</font> |


<font style="color:rgba(0, 0, 0, 0.9);">共同点：</font>

<font style="color:rgba(0, 0, 0, 0.9);">"</font>**<font style="color:rgba(0, 0, 0, 0.9);">我自己干不了，得靠别人</font>**<font style="color:rgba(0, 0, 0, 0.9);">"。</font>

<font style="color:rgba(0, 0, 0, 0.9);"></font>

<font style="color:rgba(0, 0, 0, 0.9);">不同点：</font>

<font style="color:rgba(0, 0, 0, 0.9);">pom 里写 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">mybatis-plus</font>`<font style="color:rgba(0, 0, 0, 0.9);">，是为了能用 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">BaseMapper</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 这些类；</font>

<font style="color:rgba(0, 0, 0, 0.9);">DI 说的"依赖"，是运行时 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 手里得握着一个 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserMapper</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 对象。</font>

