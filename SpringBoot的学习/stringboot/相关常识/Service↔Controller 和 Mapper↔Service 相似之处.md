---
title: Service↔Controller 和 Mapper↔Service 相似之处
url: https://www.yuque.com/ehsuh/pggizs/qbmwy2hzhrdwk8p2
doc_id: 285480122
exported_at: 2026-09-17T22:25:42
---

**<font style="color:rgba(0, 0, 0, 0.9);">依赖方只写"接口"，实现对象由外部注入。</font>**

+ **<font style="color:rgba(0, 0, 0, 0.9);">Service 层</font>**<font style="color:rgba(0, 0, 0, 0.9);">：</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserController</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">依赖</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserService</font>`<font style="color:rgba(0, 0, 0, 0.9);">（接口），实现 =</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<font style="color:rgba(0, 0, 0, 0.9);">（</font>**<font style="color:rgba(0, 0, 0, 0.9);">你自己手写</font>**<font style="color:rgba(0, 0, 0, 0.9);">）</font>
+ **<font style="color:rgba(0, 0, 0, 0.9);">Mapper 层</font>**<font style="color:rgba(0, 0, 0, 0.9);">：</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font><font style="color:rgba(0, 0, 0, 0.9);">依赖</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserMapper</font>`<font style="color:rgba(0, 0, 0, 0.9);">（接口），实现 = MyBatis 动态代理（</font>**<font style="color:rgba(0, 0, 0, 0.9);">框架自动生成，你没写</font>**<font style="color:rgba(0, 0, 0, 0.9);">）</font>

**<font style="color:rgba(0, 0, 0, 0.9);">共同点</font>**<font style="color:rgba(0, 0, 0, 0.9);">：两处都符合"面向接口 + 依赖注入"。  
</font>**<font style="color:rgba(0, 0, 0, 0.9);">不同点（唯一的）</font>**<font style="color:rgba(0, 0, 0, 0.9);">：</font>**<font style="color:rgba(0, 0, 0, 0.9);">实现类是谁造的</font>**<font style="color:rgba(0, 0, 0, 0.9);">——service层的实现类是你造，Mapper层的实现类是 MyBatis 造。</font>

