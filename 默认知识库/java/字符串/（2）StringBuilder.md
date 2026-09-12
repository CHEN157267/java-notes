---
title: （2）StringBuilder
url: https://www.yuque.com/ehsuh/oguki0/ovouskb36giusqim
doc_id: 212992125
exported_at: 2026-09-12T10:08:20
---

不需要导包

<!-- 这是一张图片，ocr 内容为：STRINGBUILDER概述 STRINGBUILLER可以看成是一个容器,创建之后里面的内容是可变的 作用:提高字符串的操作效率 容器 STRINGBUILDER对象 STRING S1 ; "AAA"; STRING S2 - "BBB"; AAABBCCCCDDD EEE STRING S3 - "CCC"; STRING S4 - "DDD"; STRING S5 "EEE"; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743300259291-37271e29-1b2d-496d-9fc9-ae0ddbfe5f7f.png)构造方法<!-- 这是一张图片，ocr 内容为：方法名 说明 创建一个空白可变字符串对象,不含有任何内容 PUBLIC STRINGBUILDER() 根据字符串的内容,来创建可变字符串对象 PUBLIC STRINGBUILDER(STRING STR) STRINGBUILDER对象 ABC STRINGBUILDER("ABC"); STRINGBUILDER SB NEW -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743300300490-bc2df71f-4f28-4514-8608-8c7d01c56c3d.png)

<!-- 这是一张图片，ocr 内容为：说明 方法名 添加数据,并返回对象本身 PUBLIC STRINGBUILDER APPEND(任意类型) 反转容器中的内容 PUBLIC STRINGBUILDER REVERSE( 返回长度(字符出现的个数) PUBLIC INT LENGTH() 通过TOSTRING()就可以实现把STRINGBUILDER转换为STRING PUBLIC STRING TOSTRING0 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743300359033-8c5e7d87-b672-45a6-a058-4e154b2f611f.png)

<!-- 这是一张图片，ocr 内容为：//2.添加字符串 SB.APPEND("AA"); SB.APPEND("BBB"); SB.APPEND("CCC"); SB.APPEND("DDD"); SYSTEM.OUT.PRINTLN(SB);//AAABBCCCDDD //3.再把STRINGBUILDER变回字符串 STRING STR - SB.TOSTRING(); SYSTEM.OUT.PRINTLN(STR);//AABBBCCCDDDD -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743300757416-2ededaf2-077d-462b-aef5-cd421dc97bea.png)

```java
//1.创建对象
stringbuilder sb = new stringbuilder("abc");
//2.添加元素
//*sb.append(1);
sb.append(2.3);
sb.append(true);
//反转
sb.reverse();
//获取长度
int len = sb.length();
system.out.println(len);
//普及：
//因为stringbuilder是java已经写好的类
//java在底层对他做了一些特殊处理。
//打印对象不是地址值而是属性值。
system.out.println(sb);
//2.添加字符串
sb.append("aa");
sb.append("bbb");
sb.append("ccc");
sb.append("ddd");
system.out.println(sb);//aaabbcccddd
//3.再把stringbuilder变回字符串
string str = sb.tostring();
system.out.println(str);//aabbbcccdddd
```

链式编程

<!-- 这是一张图片，ocr 内容为：: GETSTRING().SUBSTRING(1).REPLACE( T REPLACEMENT:"Q").LENGTH(); INT LEN TARGET: -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743300990680-5dedfa24-8623-4e4f-a922-0c1717c4d4c2.png)

```java
int len = getstring().substring(1).replace( t target: replacement:"q").length();
//getstring()是一个键盘录入数据的方法
```

依赖前一个编程的结果，再去调用后一个方法

<!-- 这是一张图片，ocr 内容为：//使用STRINGBUILDER的场景: /1.字符串的拼接 1/2.字符串的反转 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743301363169-181b8fba-4009-464a-8e94-fd1ea67f42bb.png)

StringBuilder是作为我们操作字符串的工具

<!-- 这是一张图片，ocr 内容为：展底层原理5:STRINGBUILDER源码分析 默认创建一个长度为16的字节数组 添加的内容长度小于16,直接存 添加的内容大于16会扩容(原来的容量*2+2) 如果扩容之后还不够,以实际长度为准 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743303265660-60daf523-4b3c-4e65-9673-4c7cfcb86623.png)

sb.capacity();(测容量的方法)







补充：insert

在指定位置插入值



用例：倒着录入数值

<!-- 这是一张图片，ocr 内容为：1/利用循环不断的除以2获取余数 WHILE(TRUE){ 16 IF(NUMBER BREAK; //获取余数% REMAINDAR 三 NUMBER % 2; INT //倒着拼接 SB.INSERT(OFFSET:O,REMAINDAR); //除以2 NUMBER NUMBER / 2; SB.TOSTRING( ); RETURN -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1748054110594-f8fd4292-e099-4940-8a7d-c2857bf24e9e.png)

