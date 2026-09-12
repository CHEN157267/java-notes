---
title: ArrayList
url: https://www.yuque.com/ehsuh/oguki0/sqv3wpk695zamklm
doc_id: 269969476
exported_at: 2026-09-12T10:37:18
---

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教会最实用的技术! WWW.ITHEIMA.COM ARRAYLIST 说明 构造方法 创建一个长度为0的集合 ARRAYLIST() 611611 LIBV1T&CZSEEZP13302:45/35:48 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778847139433-95da35a6-0090-49d9-933e-bcd6b9629479.jpeg)





Arraylist的方法

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教会最实用的技术! WWW.ITHEIMA.COM ARRAYLIST 方法名 说明 BOOLEAN ADD(E E) 添加数据 增 VOID ADD(INT INDEX, E E) 添加数据 删除元素 BOOLEAN REMOVE(E E) 删 删除元素 E REMOVE(INT INDEX) 改 修改元素 E SET(INT INDEX,E ) 获取元素 E GET(INT INDEX) 查 集合长度 INT SIZE() 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778847181223-9fef3e48-126c-45ff-99bc-4d41c817c74d.jpeg)



例子

<!-- 这是一张图片，ocr 内容为：一星期 VERSION CONTROL TEST1 TEST1.JAVA PROJECT CAPI-STRING CAUSERSLAWEILLDEAPROJECT PUBLIC CLASS TEST1 品 CIDEA PUBLIC STATIC VOID MAIN(STRING[] ARGS) POOREAN AAA(E E) 珍丽致猪 目 添加数据 VOID ADD(INT INDEX,E E ) 13 COM.ITHEIMA BOOLEAN REMOVE(E E) 删E元素 14 [A01APIDEMO 删除元素 E REMOVE(INT INDEX) 15 # A02STRINGDEMO E SET(INT INDEX,E ) 修改元素 16 @ A03STRINGDEMO 获取元素 E GET(INT INDEX) 17 # A04STRINGDEMO 集合长度 INTSIZE() 18 @ A05STRINGDEMO 19 A06STRINGDEMO @AO7STRINGDEMO 20 @ A08STRINGBUILDEMO //1.创建一个长度为0的ARRAYLIST集合 21 "A09TEST /// INT[]ARR - NEW INT[3];--INT 22 67A10ARRAYLISTDEMO 1/问题:能判断集合中能存储什么类型的数据吗? 23 CAT /如果没有进行限定,此时集合里面可以存储任意数据类型的数据 24 DOG 1/泛型:限定集合当中的数据类型 <数据类型> 25 STUDENT // ARRAYLIST LIST - NEW ARRAYLIST(); TEACHER 26 TEST1 27 GITIGNORE 1/用泛型去限定集合中能存储什么类型的数据 28 API-STRING.IML // ARRAYLIST<STRING> LIST - NEW ARRAYLIST<STRING>(); 29 EXTERNAL LIBRARIES // LIST.ADD("AAA"); 30 SCRATCHES AND CONSOLES 31 重复的内容:JDK7的时候,后面的泛型可以省略不写,但是见括号必须保留 32 ARRAYLIST<STRING> LIST-NEW ARRAYLIST<>(); 33 34 35 36 37 38 39 40 DAPI-STRING>C>COM>ITHEIMAIMAYLISTDEMO>LISTDEMO>T1> 33:52 4 SP ACES UTF-8 CRLF BIBU 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778847198072-264b5af6-8cf7-46f0-a90a-73db42b7d6cf.jpeg)<!-- 这是一张图片，ocr 内容为：ARRAYLIST集合 常见方法:  BOOLEAN ADD(E E) 将数据添加到末尾 将数据添加到指定位置 VOID ADD(INT INDEX,E E ) 根据元素删除 BOOLEAN REMOVE(E E) 根据索引删除 E REMOVE(INT INDEX) 将指定位置的数据,修改为新元素 E SET(INT INDEX,E ) 获取特定索引的数据 E GET(INT INDEX) 集获取合长度 INT SIZE() //1.创建一个ARRAYLIST集合的对象 ARRAYLIST<STRING> LIST ; NEW ARRAYLIST<>(); //2.添加数据 /细节1:ARRAYLIST的ADD方法不管添加什么都添加成功,忽略返回值即可 // TRUE:添加成功 FALSE:添加失败 //此时ADD方法在任意情况下,都会添加成功,永远不会失败 /因为在JAVA当中,有很多很多的集合 HASHSET(元素要唯一)  AAA(TRUE) AAA(FALSE) BILIB出 //设计:跟其他的集合保持统一(面向对象的思想) -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778847202553-ce06977d-90c3-40f3-9241-7baedbb0e292.jpeg)



<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教会最实用的技术! WWW.ITHEIMA.COM 1.什么是集合? 集合:是一种长度可变的容器 2集合有什么特点? 特点1:长度可变 总结 特点2:只能存引用数据类型,不能存基本数据类型 3.如何创建集合的对象? ARRAYLIST<STRING> LIST NEW ARRAYLIST<>(); 4.集合的常见方法? 增,删,改,查 6ILLIH SEEZ P1383547/35:48 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1778847207737-15d3c231-b9ba-418e-a8cc-8fd8677f9fd0.jpeg)

