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



`map` 接收一个函数式接口 `Function<? super T, ? extends R>`，这个函数的作用是：输入一个 T 类型的元素，返回一个 R 类型的结果。然后 `map` 会把这个函数应用到流中每个元素上，产生一个新的流，新流里的元素类型就是 R。



+ 至于方法体具体做了什么（可能是直接获取字段，也可能是复杂计算），_**对 **_`_**map**_`_** 来说不重要，它只关心输入类型和输出类型。**_

```java
List<Integer> lengths = names.stream()
.map(name -> name.length())   // String -> Integer
.collect(Collectors.toList());
```

这里 `map` 把 `String` 类型转换成了 `Integer` 类型。即使方法体里是复杂逻辑，只要最终返回的是新类型，就是 map 的工作。

