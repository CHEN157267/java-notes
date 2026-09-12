---
title: stream
url: https://www.yuque.com/ehsuh/pggizs/qwxfpkd97182vkkt
doc_id: 283818239
exported_at: 2026-09-12T09:41:11
---

Stream：像流水线一样处理集合

Stream 可以让你对集合（List、Set、Map 的 values 等）进行链式操作，就像工厂流水线：先过滤、再加工、最后收集。



stream中常见的方法是filter，map，foreach，collect，他们的作用分别是过滤，转换，打印和回流类型

其中map比较特殊：



`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">map</font>`<font style="color:rgb(15, 17, 21);"> 接收一个函数式接口 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">Function<? super T, ? extends R></font>`<font style="color:rgb(15, 17, 21);">，这个函数的作用是：输入一个 T 类型的元素，返回一个 R 类型的结果。然后 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">map</font>`<font style="color:rgb(15, 17, 21);"> 会把这个函数应用到流中每个元素上，产生一个新的流，新流里的元素类型就是 R。</font>



+ <font style="color:rgb(15, 17, 21);">至于方法体具体做了什么（可能是直接获取字段，也可能是复杂计算），</font>_**<font style="color:rgb(15, 17, 21);">对 </font>**_`_**<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">map</font>**_`_**<font style="color:rgb(15, 17, 21);"> 来说不重要，它只关心输入类型和输出类型。</font>**_

```java
List<Integer> lengths = names.stream()
.map(name -> name.length())   // String -> Integer
.collect(Collectors.toList());
```

<font style="color:rgb(15, 17, 21);">这里 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">map</font>`<font style="color:rgb(15, 17, 21);"> 把 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">String</font>`<font style="color:rgb(15, 17, 21);"> 类型转换成了 </font>`<font style="color:rgb(15, 17, 21);background-color:rgb(235, 238, 242);">Integer</font>`<font style="color:rgb(15, 17, 21);"> 类型。即使方法体里是复杂逻辑，只要最终返回的是新类型，就是 map 的工作。</font>

