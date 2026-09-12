---
title: for循环
url: https://www.yuque.com/ehsuh/oguki0/nvu8y3yyuewi8b5u
doc_id: 238660068
exported_at: 2026-09-12T10:06:23
---

<!-- 这是一张图片，ocr 内容为：FOR循环 除了WHILE循环语句外,PYTHON同样提供了FOR循环语句. 两者能完成的功能基本差不多,但仍有一些区别: WHILE循环的循环条件是自定义的,自行控制循环条件 机制,是对一批内容进行 逐个处理" FOR循环是一种"|轮询" -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758961400196-1cbcc1f4-a6d5-4126-b656-f3e4c37a6d6a.png)

与java，c语言不同，它的格式是

<!-- 这是一张图片，ocr 内容为：FOR 临时变量IN 待处理数据集: 循环满足条件时执行的代码 语法中的:待处理数据集,严格来说,称之为:序列类型 序列类型指,其内容可以一个个依次取出的一种类型,包括: 字符串 列表 元组 目前我们只学习了字符串类型,其余类型在后续章节会详细学习它们 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758962102213-cce611e9-a415-4ce0-b070-76a9a4410d6c.png)

```java
for i in 处理数据 ：
   .......
```



可用于自动变量遍历字符串

<!-- 这是一张图片，ocr 内容为：FOR循环语句 遍历字符串 #定义字符串NAME NAME"ITHEIMA" #FOR循环处理字符串 FORX IN NAMEL: PRINT(X) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758961623896-9f9fb8c5-1682-41ae-920a-67469f347126.png)

```python
for i in "asdf":
    print(i)

    s = "asdf"
for i in range(len(s)):
    print(s[i])

"结果都为
a
s
d
f
"
```

for和while语句的区别

| **<font style="color:rgb(0, 0, 0);">特性</font>** | **<font style="color:rgb(0, 0, 0);">while循环</font>** | **<font style="color:rgb(0, 0, 0);">for循环</font>** |
| :--- | :--- | :--- |
| **<font style="color:rgb(0, 0, 0);">变量更新</font>** | **<font style="color:rgb(0, 0, 0);">需</font>****<font style="color:rgb(0, 0, 0);">手动更新</font>****<font style="color:rgb(0, 0, 0);">（如</font>**`**<font style="color:rgb(0, 0, 0);">count += 1</font>**`**<font style="color:rgb(0, 0, 0);">）</font>** | **<font style="color:rgb(0, 0, 0);">自动更新</font>****<font style="color:rgb(0, 0, 0);">（由迭代器赋值）</font>** |
| **<font style="color:rgb(0, 0, 0);">循环控制</font>** | <font style="color:rgb(0, 0, 0);">依赖条件表达式</font> | <font style="color:rgb(0, 0, 0);">依赖可迭代对象长度</font> |
| **<font style="color:rgb(0, 0, 0);">风险</font>** | <font style="color:rgb(0, 0, 0);">易因未更新变量导致无限循环</font> | <font style="color:rgb(0, 0, 0);">手动修改变量无效，但无无限循环风险</font> |
| **<font style="color:rgb(0, 0, 0);">适用场景</font>** | <font style="color:rgb(0, 0, 0);">条件驱动（如用户输入、状态检测）</font> | <font style="color:rgb(0, 0, 0);">遍历数据或固定次数循环</font> |


