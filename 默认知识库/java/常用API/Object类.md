---
title: Object类
url: https://www.yuque.com/ehsuh/oguki0/lhg8rd0xxqy7v00e
doc_id: 218031284
exported_at: 2026-09-12T09:39:59
---





任意一个类的构造方法，第一行有一个隐藏的小括号，默认访问父类的无参构造，因为在顶级父类中只有无参构造，Object类是没有变量的，所以没有带参构造<!-- 这是一张图片，ocr 内容为：OBJECT的构造方法 方法名 说明 空参构造 PUBLIC OBJECT() CLASS PERSON STRING NAME; PRIVATE INT PRIVATE AGE; PUBLIC PERSON(){ SUPER(); 顶级父类中只有无参构造方法 AGE){ PUBLIC PERSON(STRING NAME, INT SUPER(); THIS.NAME 三 NAME; THIS.AGE AGEJ -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746241065171-429a81d0-cc44-460b-b476-bed773048151.png)



方法

<!-- 这是一张图片，ocr 内容为：说明 方法名 返回对象的字符串表示形式 TOSTRING PUBLIC STRING 比较两个对象是否相等 EQUALS(OBJECT OBJ) PUBLIC BOOLEAN 对象克隆 OBJECT CLONE(INT A) PROTECTED -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746241358861-6400917c-9a02-491a-bd80-cfdfc6b62ac7.png)



<!-- 这是一张图片，ocr 内容为：//细节: //SYSTEM:类名 //OUT:静态变量 //SYSTEM.OUT:获取打印的对象 /PRINTLN():方法 //参数:表示打印的内容 //核心逻辑: //当我们打印一个对象的时候,底层会调用对象的TOSTRING方法,把对象变成字符串. 1/然后再打印在控制台上,打印完毕换行处理. //思考:默认情况下,因为OBJECT类中的TOSTRING方法返回的是地址值 1/所以,默认情况下,打印一个对象打印的就是地址值 1/但是地址值对于我们是没什么意义的? 1/我想要看到对象内部的属性值?我们该怎么办? //处理方案:重写父类OBJECT类中的TOSTRING方法 SYSTEM.OUT.PRINTIN(STU);//COM.ITHEIMA.A040BJECTDEMO.STUDENT@4EEC777 //TOSTRING方法的结论: //如果我们打印一个对象,想要看到属性值的话,那么就重写TOSTRING方法就可以了. //在重写的方法中,把对象的属性值进行拼接. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746244008122-90f534c4-4994-436e-8313-d129acd74238.png)



重写例子

<!-- 这是一张图片，ocr 内容为：@OVERRIDE PUBLIC STRING TOSTRING() RETURN NAME AGEJ -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746244052570-e55260d4-0bc0-43ba-9a9e-a073e587f4fc.png)



<!-- 这是一张图片，ocr 内容为：/重写之后的EQUALS方法比较的就是对象内部的属性值了. @OVERRIDE PUBLIC BOOLEAN EQUALS(OBJECT O) { IF(THIS O) RETURN TRUE;  IF (O : NULL |L GETCLASS() 三I O.GETCLASS()) RETURN FALSE; STUDENT STUDENT (STUDENT) 0; OBJECTS.EQUALS(NAME, STUDENT.NAME); STUDENT.AGE && RETURN 三三 AGE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746245378271-c8a40b2a-ad8a-4667-84e9-c7cf2d81d23f.png)





Object类比较的是地址值

<!-- 这是一张图片，ocr 内容为：S1 ; NEW STUDENT(); STUDENT 2 ; NEW STUDENT(); STUDENT S2  BOOLEAN RESULT1 ; S1.EQUALS(S2); .N(RESULT1);//FALSE SYSTEM.OUT.PRINTLN -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746245721064-bfeff9c4-bb0c-4c55-87fc-c6624caa9427.png)





<!-- 这是一张图片，ocr 内容为：SYSTEM.OUT.PRINTLN(S.EQUALS(SB));//FALSE //因为EQUALS方法是被S调用的,而S是字符串 //所以EQUALS要看STRING类中的 //字符串中的EQUALS方法,先判断参数是否为字符串 1/如果是字符串,再比较内部的属性 1/但是如果参数不是字符串,直接返回FALSE SYSTEM.OUT.PRINTLN(SB.EQUALS(S));// FALSE //因为EQUALS方法是被SB调用的,而SB是STRINGBUILDER //所以这里的EQUALS方法要看STRINGBUILDER中的EQUALS方法 //那么在STRINGBUILDER当中,没有重写EQUALS方法 //使用的是OBJECT中的 //在OBJECT当中默认是使用--号比较两个对象的地址值 1/而这里的S和SB记录的地址值是不一样的,所以结果这回FALSE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746246680346-ca31c794-203c-41c3-940f-632efec3ea5e.png)





**<font style="color:#DF2A3F;">克隆</font>**（为protected类，想要使用就得重写）

<!-- 这是一张图片，ocr 内容为：1/2.克隆对象 //细节: //方法在底层会帮我们创建一个对象,并把原对象中的数据拷贝过去. //书写细节: /1.重写OBJECT中的CLONE方法 //2.让JAVABEAN类实现CLONEABLE接口 1/3.创建原对象并调用CLONE就可以了. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746331662274-2f0034c2-3293-4c2d-93c8-a114f44f4b90.png)

 Cloneable接口是标记性接口

<!-- 这是一张图片，ocr 内容为：/CLONEABLE 1/如果一个接口里面没有抽象方法 1/表示当前的接口是一个标记性接口 //现在CLONEABLE表示一旦了实现,那么当前类的对象就可以被克隆 //如果没有实现,当前类的对象就不能克隆 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746331883275-aedbcc62-6182-428a-bd88-24596a37a3ec.png)



（1）浅克隆

<!-- 这是一张图片，ocr 内容为：把A对象的属性值完全拷贝给B对象,也叫对象拷贝,对象复制 堆内存 ID INT 数组 0X0044 NEW STRING USERNAME 0X0011 STRING PASSWORD 0X0022 4 3 15 0X0033 STRING PATH 0X0044 INT[] DATA STRINGTABLE(串池) INT ID 1 "ZHANGSAN" STRING 0X0011 USERNAME 0X0011 对象克隆方式一 STRING PASSWORD 0X0022 "1234QWER" 0X0022 0X0033 0X0033 STRING PATH "GIRL11" 浅克隆,浅拷贝 INT[] 0X0044 DATA -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746332291734-74bc530c-1956-4d44-8c39-d1c7d9515dd6.png)



例

<!-- 这是一张图片，ocr 内容为：@OVERRIDE CLONENOTSUPPORTEDEXCEPTION OBJECT CLONE() THROWS PROTECTED //调用父类中的CLONE方法 //相当于让JAVA帮我们克隆一个对象,并把克隆之后的对象返回出去. RETURN SUPER.CLONE(); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746332922370-457cea23-ccbc-453d-bdb6-881d5b2f79c6.png)







（2）深克隆

<!-- 这是一张图片，ocr 内容为：把A对象的属性值完全拷贝给B对象,也叫对象拷贝,对象复制 堆内存 数组 0X0044 NEW ID INT 2 4 15 1 STRING USERNAME 0X0011 STRING 0X0022 PASSWORD 数组 0X0055 NEW STRING PATH 0X0033 INT[] DATA 15 4 2 0X0044 STRINGTABLE(串池) ID 1 INT STRING USERNAME 0X0011 对象克隆方式二 "ZHANGSAN" 0X0011 PASSWORD 0X0022 STRING "1234QWER" 0X0022 0X0033 STRING PATH 深克隆,深拷贝 0X0033 "GIRL11" INT[] DATA 0X0055 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746332453800-348bac0c-502c-46b9-8207-4a5d9f5ee373.png)

例

<!-- 这是一张图片，ocr 内容为：1/先把被克隆对象中的数组获取出来 INT[] DATA - THIS.DATA; //创建新的数组 INT[] NEWDATA - NEW INT[DATA.LENGTH]; //拷贝数组中的数据 (INTI ;I;I < DATA.LENGTH;I++ FOR [I] DATA[I]; NEWDATA 1/调用父类中的方法克隆对象 USER U : (USER) SUPER.CLONE(); //因为父类中的克隆方法是浅克隆,替换克隆出来对象中的数组地址值 U.DATA NEWDATA; RETURN U; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746332865914-0e8c04ee-58a1-40a4-8eeb-ef12367e3437.png)





<!-- 这是一张图片，ocr 内容为：把A对象的属性值完全拷贝给B对象,也叫对象拷贝,对象复制 浅克隆 不管对象内部的属性是基本数据类型还是引用数据类型,都完全拷贝过来 基本数据类型拷贝过来 深克隆 字符串复用 引用数据类型会重新创建新的 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746332546817-aac3d943-271b-41a6-abbf-7f62e949cc91.png)







深克隆第三方工具

<!-- 这是一张图片，ocr 内容为：GSON-2.6.2.JAR -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746333147786-44df6da2-7984-4a10-a551-784a7b23579d.png)

下载好了之后，CTRL + c 到当前模块下新建一个包，ctrl + V，右键点击 

<!-- 这是一张图片，ocr 内容为：MYAPI C:\USERS\MOON\LDEAPROJECTS\BASIC-CODEY 11 LIB GSON-2.6.2.JAR NEW SRC X CUT CTRL+X COM.ITHEIMA A01MATHDCOPY CTRL+C A02SYSTEM COPY PATH... LA03RUNTIME CTRL+V PASTE A04OBJECT FIND USAGES ALT+F7 OBJECTL ANALYZE OBJECTL REFACTOR OBJECTL ADD TO FAVORITES OBJECTL DELETE... DELETE STUDEN USER BUILD MODULE 'MYAPI' MYAPI.IML RUN'GSON-2.6.2.JAR' CTRL+SHIFT+F10 EXTERNAL LIBRARIES DEBUGSON-2.6.2.JAR SCRATCHES AND CONSO MORE RUN/DEBUG OPEN IN RIGHT SPLIT SHIFT+ENTER OPEN IN LOCAL HISTORY RELOAD FROM DISK COMPARE WITH... CTRL+D COMPARE FILE WITH EDITOR EXTERNAL TOOLS ADD AS LIBRARY ADD BOM PTG TO MYBATIS -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746333295642-b4a1fc9e-61f4-4b41-b334-36096eb4d405.png)



演示

<!-- 这是一张图片，ocr 内容为：//第三方的工具 /1.第三方写的代码导入到项目中 /2.编写代码 GSON GSON : NEW GSON(); //把对象变成一个字符串 STRING S - GSON.TOJSON(U1); //再把字符串变回对象就可以了 USER USER : GSON.FROMJSON(S,USER.CLASS); ARR : U1.GETDATA(); INT[] ARR[O] 100; //打印对象 SYSTEM.OUT.PRINTLN(USER); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746333477795-9dbef3ee-c4fd-4baa-8432-3bb359e5ab62.png)





总结

<!-- 这是一张图片，ocr 内容为：1.0BJECT是JAVA中的顶级父类. 所有的类都直接或间接的继承于OBJECT类. :一般会重写,打印对象时打印属性 2. TOSTRING( 3.EQUALS():比较对象时会重写,比较对象属性值是否相同 4.CLONE():默认浅克隆. 如果需要深克隆需要重写方法或者使用第三方工具类. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746333753795-736cca8e-cc4c-4c68-bf3d-dcda6c212dd7.png)

