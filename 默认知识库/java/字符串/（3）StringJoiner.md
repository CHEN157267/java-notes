---
title: （3）StringJoiner
url: https://www.yuque.com/ehsuh/oguki0/yrwd7pochgrk6uqa
doc_id: 212994905
exported_at: 2026-09-12T10:08:21
---

需要导包   import java.util.StringJoiner;



<!-- 这是一张图片，ocr 内容为：STRINGJOINER概述 ISTRINGJOINER眼STRINGBUILDER一样,也可以看成是一个容器,创建之后里面的内容是可变的. 作用:提高字符串的操作效率,而且代码编写特别简洁,但是目前市场上很少有人用. JDK8出现的 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743301720536-bdd83927-83ce-4ea0-b7e0-2b07e140103d.png)

<!-- 这是一张图片，ocr 内容为：STRINGJOINER 的构造方法 方法名 说明 创建一个STRINGJOINER对象,指定拼接时的间隔符号 PUBLIC STRINGJOINER (间隔符号) 创建一个STRINGJOINER对象,指定拼接时的间隔符号, PUBLIC STRINGJOINER (间隔符号,开始符号,结束符号) 开始符号,结束符号 1---2---3 STRINGJOINER SJ - NEW STRINGJOINER("---"); [1, 2, 3] STRINGJOINER SJ - NEW STRINGJOINER(", ","["["]"); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743301775861-2c82db6b-446d-4ed9-b1c7-0da674ac7d7f.png)

<!-- 这是一张图片，ocr 内容为：STRINGJOINER的成员方法 方法名 说明 添加数据,并返回对象本身 PUBLIC STRINGJOINER ADD (添加的内容) 返回长度(字符出现的个数) PUBLIC INT LENGTH() 返回一个字符串(该字符串就是拼接之后的结果) PUBLIC STRING TRING0 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743301820542-d2f819fd-c932-4493-8921-dcc83620a8a8.png)<!-- 这是一张图片，ocr 内容为：/11.创建对象 STRINGJOINER SJ - NEW STRINGJOINER( DELIMITER:", ", PREFIX:"[", SUFFIX:"]); 1/2.添加元素 SJ.ADD("AAA").ADD("BBB").ADD("CCC"); INT LEN - SJ.LENGTH(); SYSTEM.OUT.PRINTLN(LEN);//15 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743301982677-ed52f877-6b7f-4831-8c81-caa2c1f3f66d.png)

```java
//1.创建对象
StringJoiner sj = new StringJoiner( delimiter:", ", prefix:"[", suffix:"]);
//2.添加元素
sj.add("aaa").add("bbb").add("ccc");
int len = sj.length();
system.out.println(len);//15
```

int len = sj.length();//表示的是字符的个数（也算上间隔符号，开始标记，结束标记）

