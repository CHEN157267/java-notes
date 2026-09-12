---
title: （1）String
url: https://www.yuque.com/ehsuh/oguki0/zs684lnrp0wlfs11
doc_id: 212987011
exported_at: 2026-09-12T09:40:55
---



_**<font style="color:#DF2A3F;">在 Java 中，</font>**_`_**<font style="color:#DF2A3F;">equals</font>**_`_**<font style="color:#DF2A3F;">方法在</font>**_`_**<font style="color:#DF2A3F;">String</font>**_`_**<font style="color:#DF2A3F;">类中被重写了，它比较的是字符串的内容，而不是地址值。</font>**_<!-- 这是一张图片，ocr 内容为：字符串比较 BOOLEAN EQUALS方法(要比较的字符串) 完全一样结果才是TRUE,否则为FALSE 忽略大小写的比较 BOOLEAN EQUALSLGNORECASE(要比较的字符串) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743297983393-0a801eaa-dd02-4f9d-8cd8-66ea42f986ef.png)<!-- 这是一张图片，ocr 内容为：需求:键盘录入一个字符串,使用程序实现在控制台遍历该字符串 PUBLIC CHAR CHARAT(INDEX):根据索引返回字符 PUBLIC INTLENGTH():返回此字符串的长度 数组的长度:数组名.LENGTH 字符串的长度:字符串对象.LENGTH() "钢门123吹小雪" 长度:8 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743298085192-b3fff1a9-cf5b-4c1c-a8c8-92fc4957764e.png)

<!-- 这是一张图片，ocr 内容为：截取 STRING SUBSTRING(INT BEGINLNDEX, INT ENDLNDEX) 包头不包尾,包左不包右 注意点: 只有返回值才是截取的小串 截取到末尾 STRING SUBSTRING(INT BEGINLNDEX) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743299226429-aa6669b7-a687-4dc5-b6c1-f05dc4690ef7.png)

对原来调用者的字符串没有任何影响

截取单个也可以用charAt

<!-- 这是一张图片，ocr 内容为：STRING REPLACE(旧值,新值)替换 注意点:只有返回值才是替换之后的结果 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743299653925-c800d25d-f66a-4a8f-9869-aa88f5c03ade.png)

<!-- 这是一张图片，ocr 内容为：/1.获取到说的话 STRING TALK ;你玩的真好,以后不要再玩了,TMD,CNM"; 1/2.定义一个敏感词库 STRING[] ARR 三 {"TMD","CNM","SB","MLGB"}; 1/3.循环得到数组中的每一个敏感词,依次进行替换 FOR (INTI ;I < ARR.LENGTH;I++){ TALK TALK.REPLACE(ARR[I],REPLACEMENT:"**"); 子 //4.打印结果 SYSTEM.OUT.PRINTLN(TALK); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743299860429-ef14a605-8b2f-42b7-af04-647b697555ba.png)

```java
//获取到说的话
string talk = "你玩的真好，以后不要再玩了，tmd,cnm";
//2.定义一个敏感词库
string[] arr 三 {"tmd","cnm","sb","mlgb"};
//3.循环得到数组中的每一个敏感词，依次进行替换
for (int i ;i < arr.length;i++){
    talk talk.replace(arr[i],replacement:"***");
}
    //4.打印结果
    system.out.println(talk);
```



<!-- 这是一张图片，ocr 内容为：STRING的注意点 字符串的内容是不会发生改变的,它的对象在创建后不能被更改. "尼古拉斯?阿玮"; STRING NAME STRING  SCHOOLNAME ;黑马程序员"; 字符串拼接产生一个新的字符串 SYSTEM.OUT.PRINTLN(NAME + SCHOOLNAME); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742440700892-f71f5964-9550-4e21-9e1e-332d68824e64.png)

<!-- 这是一张图片，ocr 内容为：1.STRIN是JAVA定义好的一个类.定义在JAVA.LANG包中, 所以使用的时候不需要导包. 2.JAVA程序中的所有字符串文字(例如"ABCDEFG") 都被实为此类的对象. 3.字符串不可变,它们的值在创建后不能被更改 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742440371506-ae102052-7e2a-4e3a-9e5d-e236f645ee7a.png)

例子

<!-- 这是一张图片，ocr 内容为：-"尼古拉斯.阿玮"; STRING 三 NAME NAME"三连加投币阿玮"; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742692148731-45e9b6bf-3d91-4854-b5c2-1289a1a77f1b.png)

它并没有改变字符串，而是创建了一个新的字符串，将新的字符串赋值给了name



<!-- 这是一张图片，ocr 内容为：1.STRIN是JAVA定义好的一个类.定义在JAVA.LANG包中, 所以使用的时候不需要导包. 总结 2.JAVA程序中的所有字符串文字(例如"ABCDEFG"). 都被实为此类的对象. 3.字符串不可变,它们的值在创建后不能被更改 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742692277129-37b85f73-b9c1-417b-84ae-cbc59d21ad55.png)

String的构造方法

<!-- 这是一张图片，ocr 内容为：1/1.使用直接赋值的方式获取一个字符串对象 STRING S1 - "ABC"; SYSTEM.OUT.PRINTLN(S1);//ABC 1/2.使用NEW的方式来获取一个字符串对象 1/空参构造:可以获取一个空白的字符串对象 STRING S2 - NEW STRING(); SYSTEM.OUT.PRINTLN("@" + S2 + "!");//""" 1/传递一个字符串,根据传递的字符串内容再创建一个新的字符串对象 STRING S3 NEW STRING(ORIGINAL:"ABC"); SYSTEM.OUT.PRINTLN(S3); 1/传递一个字符数组,根据字符数组的内容再创建一个新的字符串对象 1/需求:我要修改字符串的内容. ABC QBC  //ABC --> {'A','B','C'} > {'Q','B','C'} --> "QBC"  CHAR[] CHS :{'A','B','C','D'}; ; NEW STRING(CHS); STRING S SYSTEM.OUT.PRINTLN(S4);//ABCD -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742692581665-6b14be1a-8712-4348-b2bc-fd58ac6f3a97.png)

<!-- 这是一张图片，ocr 内容为：1/传递一个字节数组,根据字节数组的内容再创建一个新的字符串对象 BYTE[] BYTES ; {97, 98, 99, 100}; STRING(BYTES); STRING S5 3 NEW SYSTEM.OUT.PRINTLN(S5);//ABCD -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742692691611-0169ab1c-3c49-463b-a849-5eacc531e1ed.png)

先用ASCII码表将数字转化为字母

<!-- 这是一张图片，ocr 内容为：网络当中传输的数据其实都是字节信息 1/我们一般要把字节信息进行转换,转成字符串,此时就要用到这个构造了 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742692774583-a8d51545-dc91-49eb-aba0-a5256b03f679.png)



<!-- 这是一张图片，ocr 内容为：堆内存 栈内存 NEW出来的对象 都在这里 方法运行的时候进栈 UBLIC CLASS STRINGDEMO { 执行完毕出栈 PUBLIC STATIC VOID MAIN(STRING[] ARGS) { STRING S1 -"ABC'; STRINGTABLE(串池) STRING S2 : "ABC"; 方法:MAIN() STRINGS10X0011 暗中观察 STRING S2 0X0011 "ABC"0X0011 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742693261819-fab10b9f-732e-49a9-aa6d-a9504e06f9ce.png)

<!-- 这是一张图片，ocr 内容为：当使用双引号直接赋值时,系统会检查该字符串在串池中是否存在. 不存在:创建新的 存在:复用 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742693204827-a3bf9bd4-1b64-40a9-b957-573ec38cc1b4.png)



<!-- 这是一张图片，ocr 内容为：PUBLIC TEST CLASS 堆内存 栈内存 PUBLIC STATIC VOID MAIN(STRING[] ARGS){  CHAR[] CHS ;{'A', 'B', 'C'}; 方法:MAIN STRING S1 - NEW STRING(CHS); STRING S2- NEW STRING(CHS); CHARL CHS 子 0X0011 "ABC" STRING S1 0X0022 STRING S2 'ABC" 0X0033 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742693507374-bb0d3a13-7c62-4653-85c0-8f85e5eb342b.png)

直接赋值是一样  引用的不一样

这里堆内存因为有new，所以会再建一个新内存，直接赋值有复用，而 引用赋值则会新建新空间







**<font style="color:#DF2A3F;">包头不包尾” 原则仅适用于 双参数 的 </font>**`**<font style="color:#DF2A3F;">substring</font>**`**<font style="color:#DF2A3F;"> 方法（即 </font>**`**<font style="color:#DF2A3F;">substring(beginIndex, endIndex)</font>**`**<font style="color:#DF2A3F;">）。</font>**

