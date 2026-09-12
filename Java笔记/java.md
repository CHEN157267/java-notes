---
title: java
url: https://www.yuque.com/ehsuh/oguki0/ffs0q0bi3gstsydr
doc_id: 204956923
exported_at: 2026-09-12T10:37:51
---

<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">抽象类作为形参</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">完全支持多态</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">，通过子类继承和方法重写实现运行时动态绑定。其与接口多态的核心区别在于：</font>

+ **<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">抽象类</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">：强调整合（共享属性/逻辑），适合</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">同源子类</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">的扩展。</font>
+ **<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">接口</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">：强调行为契约，适合</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">跨体系功能组合</font>**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">。</font>

<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);">实际开发中，若子类有显著共性逻辑，优先用抽象类；若需解耦行为定义，或支持多重能力，则用接口。两者互补，共同构成 Java 多态的核心机制</font>

<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(252, 252, 252);"></font>

<font style="color:rgba(0, 0, 0, 0.9);background-color:rgb(243, 243, 243);">对象1.方法（对象2）</font>

+ `**<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);">this</font>**`**<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);"> 永远绑定调用者</font>**<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);">（</font>`<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);">对象1</font>`<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);">），与参数无关。</font>

<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);"></font>

<font style="color:rgba(0, 0, 0, 0.4);background-color:rgb(252, 252, 252);">对象引用 instanceof 类/接口</font>

