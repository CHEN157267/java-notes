---
title: 关于对@Mapper的理解
url: https://www.yuque.com/ehsuh/pggizs/zg0gwegpw4gvdvw5
doc_id: 285429583
exported_at: 2026-09-17T22:25:51
---

`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">Mapper</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">层中，被@Mapper注释标记的文件</font><font style="color:rgba(0, 0, 0, 0.9);"> 是个 interface → MyBatis 在运行时用 JDK 动态代理生成了一个实现类 → Spring 把它当 bean 放进容器 → 你在 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImpl</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 里 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Autowired UserMapper</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 就能拿到它。</font>

