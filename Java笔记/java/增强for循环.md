---
title: 增强for循环
url: https://www.yuque.com/ehsuh/oguki0/dk3get7x144h8mtf
doc_id: 219659000
exported_at: 2026-09-12T10:38:18
---

**增强 for 循环（Enhanced For Loop）的设计初衷是为了简化数组和集合的遍历**，但它的适用范围不仅限于此。本质上，**只要对象实现了 **`**Iterable**`** 接口**（提供 `iterator()` 方法），或者是**数组**，就可以使用增强 for 循环。



### 一、**基础用法：遍历数组和集合**
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







#### 2. **集合（Collection）**
所有实现了 `java.util.Collection` 接口的类（如 `**<u>ArrayList</u>**`、`LinkedList`、`HashSet` 等）都默认实现了 `Iterable` 接口，因此可以直接使用增强 for 循环：

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







### **扩展用法：遍历实现**** **`**Iterable**`** ****接口的任意对象**
如果自定义类实现了 `Iterable` 接口并提供 `iterator()` 方法，也可以使用增强 for 循环遍历其元素。 



**关键点**：

+ `Iterable` 接口要求类必须实现 `iterator()` 方法，返回一个 `Iterator` 对象。
+ 增强 for 循环本质上会调用 `iterator()` 方法，并通过 `hasNext()` 和 `next()` 方法迭代元素。



#### **非 Iterable 且非数组的对象**
**如果一个类既不是数组，也没有实现 **`**Iterable**`** 接口，则无法直接使用增强 for 循环。**











