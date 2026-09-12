---
title: System类
url: https://www.yuque.com/ehsuh/oguki0/xurzu7tgd52kn24a
doc_id: 217963410
exported_at: 2026-09-12T10:38:16
---

<!-- 这是一张图片，ocr 内容为：SYSTEM SYSTEM也是一个工具类,提供了一些与系统相关的方法 方法名 说明 终止当前运行的 虚拟机 PUBLIC STATIC VOID EXIT(INT STATUS) JAVA 返回当前系统的时间毫秒值形式 PUBLIC STATIC LONG CURRENTTIMEMILLIS() PUBLIC STATIC VOID ARRAYCOPY(数据源数组,起始索 数组拷贝 引,目的地数组,起始索引,拷贝个数) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746156697197-d40c1976-6921-427f-9c94-8c8cd23826cf.png)

currentTimeMillis()的起始时间是1970.1.1



<!-- 这是一张图片，ocr 内容为：1/方法的形参: //状态码: 1/0:表示当前虚拟机是正常停止 1/非日:表示当前虚拟机异常停止 SYSTEM.EXIT( STATUS:0); SYSTEM.OUT.PRINTLN("看看我执行了吗?"); //以拼图小游戏为例: //当我们需要把整个程序就结束的时候,就可以调用这个方法. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746156847128-714d2f17-77c6-4cae-9363-9dc5f89d33c3.png)

无论exit（）的括号里面是否是零，程序运行到这都会停止



可以通过currentTimeMillis()获取程序的运行时间（单位是毫秒）

<!-- 这是一张图片，ocr 内容为：MAIN(STRING[] ARGS){ PUBLIC STATIC VOID //判断1~1000之间有多少个质数 ART - SYSTEM.CURRENTTIMEMILLIS(); LONG START FOR (INTI - 1;I < 10000;I++) BOOLEAN FLAG 三 ISPRIME1(I); IF(FLAG) SYSTEM.OUT.PRINTLN(I); SYSTEM.CURRENTTIMEMILLIS(); LONG END P //获取程序运行的总时间 SYSTEM.OUT.PRINTLN(END START); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746157123513-3da81c2a-7019-48e0-8812-fc929b6bc1a3.png)





<!-- 这是一张图片，ocr 内容为：//拷贝数组 INT[] ARR1 {1,2 {1,2,3,4,5,6,7,8,9,10]; INT[10]; INT[] ARR2 NEW INT //把ARR1数组中的数据拷贝到ARR2中 1/参数一:数据源,要拷贝的数据从哪个数组而来 1/参数二:从数据源数组中的第几个索引开始拷贝 1/参数三:目的地,我要把数据拷贝到哪个数组中 1/参数四:目的地数组的索引. 1/参数五:拷贝的个数 SYSTEM.ARRAYCOPY(ARR1, SRCPOS:O,ARR2, DESTPOS:0,LENGTH:10); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746157400003-7b9be49c-b76e-49ab-97ef-10710769be94.png)

<!-- 这是一张图片，ocr 内容为：//1.如果数据源数组和目的地数组都是基本数据类型,那么两者的类型必须保持一致,否则会报错 1/2.在拷贝的时候需要考虑数组的长度,如果超出范围也会报错 /3.如果数据源数组和目的地数组都是引用数据类型,那么子类类型可以赋值给父类类型 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746157856089-5db046d0-3761-4cb3-9670-93541423642e.png)

但是需要强制转换



<!-- 这是一张图片，ocr 内容为：STUDENT( HAME:"ZHANGSAN",AGE:23); STUDENT S1 NEW STUDENT(NAME:"LISI",AGE:24); STUDENT S2 NEW 三 NEW STUDENT( NAME:"WANGWU", AGE: 25); STUDENT S3 三 STUDENT[]ARR1 ;{S1, S2, S3]; PERSON[] ARR2 NEW PERSON[3]; //把ARR1中对象的地址值赋值给ARR2中 SYSTEM.ARRAYCOPY(ARR1,SRCPOS:0,ARR2, DESTPOS: O,LENGTH:3); //遍历数组ARR2 FOR (INT I ; I < ARR2.LENGTH; I++){ STUDENT STU - (STUDENT) ARR2[I]; SYSTEM.OUT.PRINTIN(STU.GETNAME() + ", "+ STU.GETAGE()); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746157834388-c276af27-0d5b-426f-9543-6da4946553c8.png)

