---
title: String赋值的区别
url: https://www.yuque.com/ehsuh/oguki0/am9g9v4oktgdzntx
doc_id: 269968543
exported_at: 2026-09-12T09:31:48
---

直接赋值的内存结构

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教会最实用的技术! WWW.ITHEIMA.COM 直接赋值的内存结构 MEMORYJAVA PUBLIC CLASS MEMORY STRING TABLE(串池) 暗中观察 PUBLIC STATIC VOID MAIN(STRING[] ARGS){ "ABC" OX0011 STRING S1 "ABC"; STRING S2-"ABC"; MAIN 复用字符串 STRING S1 堆内存 ........... 0X0011 注意点: STRING MEMORY.C1ASS 双引号直接赋值的时候,会检查串池 0X0011 MAIN 不存在:创建新的 存在:复用 栈内存 方法区 LILLIT 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778846302079-4a665565-1726-4d54-b844-0538e9ae9a88.jpeg)



new出来字符串的内存结构

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教会最实用的技术! WWW.ITHEIMA.COM NEW出来字符串的内存结构 STRING TABLE(串池) "ABC" 0X0011 MEMORY.JAVA MAIN STRING PUBLIC CLASS MEMORY { 0X0022 PUBLIC STATIC VOID MAIN(STRING[] ARGS) { 0X0011 STRING S "ABC"; "ABC" STRING S1- NEW STRING(S); STRING S1 STRING S2 NEW STRING(S); 0X0033 0X0022 子 "ABC" STRING 0X0033 堆内存 栈内存 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778846316105-aadd1b95-56eb-412d-9406-49a555a0e060.jpeg)



有两种定义字符串的方式，第一种是直接定义，第二种是new关键字

第一种定义字符串的时候，会在堆内存中的串池中（jdk7之后在堆内存，jdk7之前在方法区）寻找是否有这个字符串，有的话，会直接传递地址，没有的话，会创建新的，如果多个字符串类型的值相同的话，它们的地址也会相同。

第二种定义方式无论是否值相同，它们的地址都不同

.equals是检查地址是否相同

