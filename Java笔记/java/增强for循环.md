---
title: 增强for循环
url: https://www.yuque.com/ehsuh/oguki0/dk3get7x144h8mtf
doc_id: 219659000
exported_at: 2026-09-12T10:38:18
---

**<font style="color:rgb(0, 0, 0) !important;">增强 for 循环（Enhanced For Loop）的设计初衷是为了简化数组和集合的遍历</font>**<font style="color:rgba(0, 0, 0, 0.85);">，但它的适用范围不仅限于此。本质上，</font>**<font style="color:rgb(0, 0, 0) !important;">只要对象实现了 </font>**`**<font style="color:rgb(0, 0, 0);">Iterable</font>**`**<font style="color:rgb(0, 0, 0) !important;"> 接口</font>**<font style="color:rgba(0, 0, 0, 0.85);">（提供 </font>`<font style="color:rgba(0, 0, 0, 0.85);">iterator()</font>`<font style="color:rgba(0, 0, 0, 0.85);"> 方法），或者是</font>**<font style="color:rgb(0, 0, 0) !important;">数组</font>**<font style="color:rgba(0, 0, 0, 0.85);">，就可以使用增强 for 循环。</font>



### <font style="color:rgb(0, 0, 0);">一、</font>**<font style="color:rgb(0, 0, 0) !important;">基础用法：遍历数组和集合</font>**
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) { // 遍历基本类型数组
    System.out.println(num);
}

String[] names = {"Alice", "Bob", "Charlie"};
for (String name : names) { // 遍历引用类型数组
    System.out.println(name);
}
```







#### <font style="color:rgb(0, 0, 0);">2.</font><font style="color:rgb(0, 0, 0);"> </font>**<font style="color:rgb(0, 0, 0) !important;">集合（Collection）</font>**
<font style="color:rgba(0, 0, 0, 0.85) !important;">所有实现了 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">java.util.Collection</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 接口的类（如 </font>`**<u><font style="color:#DF2A3F;">ArrayList</font></u>**`<font style="color:rgba(0, 0, 0, 0.85) !important;">、</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">LinkedList</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">、</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">HashSet</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 等）都默认实现了 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Iterable</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 接口，因此可以直接使用增强 for 循环：</font>

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
for (String element : list) { // 遍历 List
    System.out.println(element);
}

Set<Integer> set = new HashSet<>();
set.add(1);
set.add(2);
for (Integer num : set) { // 遍历 Set
    System.out.println(num);
}
```







### **<font style="color:rgb(0, 0, 0) !important;">扩展用法：遍历实现</font>****<font style="color:rgb(0, 0, 0) !important;"> </font>**`**<font style="color:rgb(0, 0, 0);">Iterable</font>**`**<font style="color:rgb(0, 0, 0) !important;"> </font>****<font style="color:rgb(0, 0, 0) !important;">接口的任意对象</font>**
<font style="color:rgba(0, 0, 0, 0.85) !important;">如果自定义类实现了 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Iterable</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 接口并提供 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">iterator()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 方法，也可以使用增强 for 循环遍历其元素。 </font>

<font style="color:rgba(0, 0, 0, 0.85) !important;"></font>

**<font style="color:rgb(0, 0, 0) !important;">关键点</font>**<font style="color:rgba(0, 0, 0, 0.85) !important;">：</font>

+ `<font style="color:rgb(0, 0, 0);">Iterable</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> </font><font style="color:rgba(0, 0, 0, 0.85) !important;">接口要求类必须实现</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgb(0, 0, 0);">iterator()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> </font><font style="color:rgba(0, 0, 0, 0.85) !important;">方法，返回一个</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgb(0, 0, 0);">Iterator</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> </font><font style="color:rgba(0, 0, 0, 0.85) !important;">对象。</font>
+ <font style="color:rgba(0, 0, 0, 0.85) !important;">增强 for 循环本质上会调用 </font>`<font style="color:rgb(0, 0, 0);">iterator()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 方法，并通过 </font>`<font style="color:rgb(0, 0, 0);">hasNext()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 和 </font>`<font style="color:rgb(0, 0, 0);">next()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 方法迭代元素。</font>



#### **<font style="color:rgb(0, 0, 0) !important;">非 Iterable 且非数组的对象</font>**
**<font style="color:#DF2A3F;">如果一个类既不是数组，也没有实现 </font>**`**<font style="color:#DF2A3F;">Iterable</font>**`**<font style="color:#DF2A3F;"> 接口，则无法直接使用增强 for 循环。</font>**











