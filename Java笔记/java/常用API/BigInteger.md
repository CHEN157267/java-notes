---
title: BigInteger
url: https://www.yuque.com/ehsuh/oguki0/fo7sddw22rg5qn0n
doc_id: 218583081
exported_at: 2026-09-12T10:38:13
---

_**<font style="color:#DF2A3F;">对象一旦创建，内部记录的值是无法改变的</font>**_

<!-- 这是一张图片，ocr 内容为：说明 方法名 获取随机大整数,范围:[0 ~2的NUM次方-1] PUBLIC BIGINTEGER(INT NUM, RANDOM RND) 获取指定的大整数 PUBLIC BIGINTEGER(STRING VAL) 获取指定进制的大整数 PUBLIC BIGINTEGER(STRING VAL, INT RADIX) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746621063783-60ab82c0-18c6-4213-8e8a-e0aa7a18513a.png)

<!-- 这是一张图片，ocr 内容为：静态方法获取BIGINTEGER的对象,内部有优化 PUBLIC STATIC BIGINTEGER VALUEOF(LONG VAL) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746621353006-86415634-6c41-4a0c-93ed-c12a03698478.png)上图中的String val必须是整数，不然会报错

int radix是表示几进制



用例：

<!-- 这是一张图片，ocr 内容为：RANDOM(); RANDOM NEW BIGINTEGER( NUMBITS:4,R); ER BD1 NEW BIGIR BIGINTEGER SYSTEM.OUT.PRINTLN(BD1); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746621651895-10a0c274-1c11-4c76-8693-09fca77a9479.png)

<!-- 这是一张图片，ocr 内容为：/1.获取一个随机的大整数 RANDOM R NEW RANDOM(); /* FOR(INTI ZI;I00;I+++++){ BIGINTEGER BD1 - NEW BIGINTEGER(4,R); SYSTEM.OUT.PRINTLN(BD1);//[E ~15] 丁*/ 1/2.获取一个指定的大整数 //细节:字符串中必须是整数, 否则会报错 BIGINTEGER BD2 - NEW BI BIGINTEGER(VAL:"9223372036854775808"): SYSTEM.OUT.PRINTLN(BD2); BIGINTEGER BD3 NEW BIGINTEGER("ABC"); SYSTEM.OUT.PRINTLN(BD3);*/ //3,获取指定进制的大整数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746842875941-65b3a566-a18b-4aa8-8d1d-46bd0f43b833.png)

<!-- 这是一张图片，ocr 内容为：外比巴卜 32 SYSTEM.OUT.PRINTLN(BD3) 33 /3.获取指定进制的大整数 34 //细节: 35 /1.字符串中的数字必须是整数 36 1/2.字符串中的数字必须要跟进制吻合. 37 1/比如二进制中,那么只能写O和1,写其他的就报错. 38 /*BIGINTEGER BD4 - NEW BIGINTEGER("123",2); 39 SYSTEM.OUT.PRINTLN(BD4);*/ 40 41 1/4.静态方法获取BIGINTEGER的对象,内部有优化 42 //细节: 43 /1.能表示范围比较小,在1ONG的取值范围之类,如果超出LONG的范围就不行了. 44 BIGINTEGER BD5 - BIGINTEGER.VALUEOF(9223372036854775808L) 45 46 SYSTEM.OUT.PRINTLN(BD5); 47 48 -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746842851776-5175389c-872b-4ce9-a449-2876f47bfdad.jpeg)

补充：

<!-- 这是一张图片，ocr 内容为：/4.静态方法获取BIGINTEGER的对象,内部有优化 //细节: //1.能表示范围比较小,只能在1ONG的取值范围之内,如果超出1ONG的范围就不行了. /2.在内部对常用的数字: -16~16进行了优化. //提前把-16 .16先创建好BIGINTEGER的对象,如果多次获取不会重新创建新的. BIGINTEGER BD5 - BIGINTEGER.VALUEOF(16); BIGINTEGER BD6 - BIGINTEGER.VALUEOF(16); SYSTEM.OUT.PRINTLN(BD5 - BD6);//TRUE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746844373880-532f7dba-e363-43e6-9c04-b03acca89ba2.png)

<!-- 这是一张图片，ocr 内容为：BIGINTEGER BD8 ; BIGINTEGER.VALUEOF(17); SYSTEM.OUT.PRINTLN(BD7 - BD8);//FALSE*/ 1/5,对象一旦创建内部的数据不能发生改变 BIGINTEGER BD9 - BIGINTEGER.VALUEOF(1); BIGINTEGER BD10 BIGINTEGER.VALUEOF(2); BIGINTEGER RESULT : BD9.ADD(BD10); SYSTEM.OUT.PRINTLN(RESULT);//3 //此时,不会修改参与计算的BIGINTEGER对象中的值,而是产生了一个新的BIGINTEGER对象记录3 -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746842896682-7bf88aa3-e2fc-4473-8b64-b71892cce56e.jpeg)





小结

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用最短时间,教 WWW.ITHEIMA.COM BIGLNTEGER构造方法小结 如果BIGINTEGER表示的数字没有超出LONG的范围,可以用静态方法获取. 如果BIGINTEGER表示的超出LONG的范围,可以用构造方法获取. 对象一旦创建,BIGINTEGER内部记录的值不能发生改变. R对 只要进行计算都会产生一个新的BIGINTEGER对象 -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746842928574-5b748aac-170c-426d-830a-ec27714a3759.jpeg)







关于BigInteger的计算

<!-- 这是一张图片，ocr 内容为：EXTERNAL LIBRARIES //1.创建两个BIGINTEGER对象 20 SCRATCHES AND CONSOLES BIGINTEGER BD1 BIGINTEGER.VALUEOF(10); 21 BIGINTEGER BD2 BIGINTEGER.VALUEOF(3); 22 23 //2.加法 24 BIGINTEGER BD3 : BD1.ADD(BD2); 25 26 SYSTEM.OUT.PRINTLN(BD3); 27 28 //3.除法,获取商和余数 BIGINTEGER[] ARR - BD1.DIVIDEANDREMAINDER(BD2); 29 SYSTEM.OUT.PRINTLN(ARR[E]); 30 SYSTEM.OUT.PRINTLN(ARR[1]); 31 32 2.0 BIGLNTEGERDEMO2 RUN: F;JDEVEJOP)JOK(BIN)JAVA.EXE -JAVABENT:JERU5587ELOP(IDEA/INTEJLIJIDEAZOZ3.INI,INL,INT,JERU55878:F; 小小小中中面 ISTRUCTURE 13 AVORITES -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746842972200-10ba8205-1208-4d15-a640-3900a9a4561e.jpeg)

除法： 数组的零所引是商，一所引是余



<!-- 这是一张图片，ocr 内容为：//4.比较是否相同 BOOLEAN RESULT:BD1.EQUALS(BD2); SYSTEM.OUT.PRINTLN(RESULT); //5.次幂 BIGINTEGER BD4 BD1.POW(2); SYSTEM.OUT.PRINTLN(BD4); //6.MAX BIGINTEGER BD5-BD1.MAX(LD2); SYSTEM.OUT.PRINTLN(BD5 BD1);//TRUE BD2);//FALSE SYSTEM.OUT.PRINTLN(BD5 BD2 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746843029586-38d4a356-9a51-4bc9-ad02-1d4fc9da0b4f.png)

在BigInteger中，Max方法得到的不是新建的对象



<!-- 这是一张图片，ocr 内容为：1/7.转为INT类型整数,超出范围数据有误 BIGINTEGER BD6 - BIGINTEGER.VALUEOF(2147483647L); /*  BIG INT I - BD6.INTVALUE(); SYSTEM.OUT.PRINTLN(I);*/ BIGINTEGER BD6 BIGINTEGER.VALUEOF(200); DOUBLEVALBD6.DOUBLEVALUE(); SYSTEM.OUT.PRINTLN(V); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746843055526-f3d08c13-f2c7-484f-baf9-48d99e6ab7d8.png)转化：将BigInteger转化为其他基本数据类型





<!-- 这是一张图片，ocr 内容为：1.BIGLNTEGER表示一个大整数. 2.如何获取BIGLNTEGER的对象? BIGLNTEGER B1GLNTEGER.VALUEOF(0.1); 总结 BIGLNTEGER B1 NEW BIGLNTEGER("整数"); 3.常见操作 减:SUBTRACT 加:ADD 除:DIVIDE,DIVIDEANDREMAINDER 乘:MULTIPLY 比较:EQUALS,MAX,MIN 次幂:POW 转成整数:INTVALUE,LONGVALUE -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746843304068-d9efbfcb-ec21-44fe-9d8c-f3fdf8b44248.jpeg)





