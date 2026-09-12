---
title: SimpleDateFormat 格式化时间
url: https://www.yuque.com/ehsuh/oguki0/ayihf9g5vdtruhzu
doc_id: 219970656
exported_at: 2026-09-12T10:07:29
---

<!-- 这是一张图片，ocr 内容为：SIMPLEDATEFORMAT类作用 格式化:把时间变成我们喜欢的格式. 解析:把字符串表示的时间变成DATE对象. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747449482429-a0becd49-2091-4e5d-9310-9cf17e72d8c2.png)



<!-- 这是一张图片，ocr 内容为：说明 构造方法 构造一个SIMPLEDATEFORMAT,使用默认格式 PUBLIC SIMPLEDATEFORMAT() 构造一个SIMPLEDATEFORMAT,使用指定的格式 PUBLIC SIMPLEDATEFORMAT(STRING PATTERN) 说明 常用方法 格式化(日期对象 -> 字符串) PUBLIC FINAL STRING FORMAT(DATE DATE) 解析(字符串->日期对象) PUBLIC DATE PARSE(STRING SOURCE) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747449570423-3dc7f660-f0a6-4590-bca5-f91d0a45c423.png)



<!-- 这是一张图片，ocr 内容为：格式化的时间形式的常用的模式对应关系如下: 年月 Y M 2023-11-11 13:27:06 2023年11月11日 13:27:06 日时分秒 P H YYYY年MM月DD日 HH:MM:SS YYYY-MM-DD HH:MM:SS M S -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747449778886-78c3d848-3b3f-4ad1-a8c5-0f39f01dd8ea.png)





format方法的应用（默认情况和指定情况）

<!-- 这是一张图片，ocr 内容为：/1.利用空参构造创建SIMPLEDATEFORMAT对象,默认格式 SIMPLEDATEFORMAT SDF1 - NEW SIMPLEDATEFORMAT(); DATE D1 : NEW DATE(OL); STRING STR1 - SDF1.FORMAT(D1); 上午8:00 SYSTEM.OUT.PRINTLN(STR1);//1970/1/1 /2.利用带参构造创建SIMPLEDATEFORMAT对象,指定格式 SIMPLEDATEFORMAT SDF2 - NEW SIMPLEDATEFORMAT( PATTERN:"YYYYYYY$MM月DD日 HH:MMISS EE"); R2 SDF2.FORMAT(D1); STRING STR2 SYSTEM.OUT.PRINT1N(STR2);//1970年01月01日 08:00:00 //课堂练习:YYY年MM月DD日 时:分:秒 星期E -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747450306084-4590a957-5770-4479-9784-3def253d8d84.png)





parse方法的应用（字符串转Date类对象的变量）

<!-- 这是一张图片，ocr 内容为：1/1.定义一个字符串表示时间 STRING STR "2023-11-11 11:11:11"; /2.利用空参构造创建SIMPLEDATEFORMAT对象 //细节: 1/创建对象的格式要跟字符串的格式完全一致 SIMPLEDATEFORMAT SDF - NEW SIMPLEDATEFORMAT( PATTERN:"YYYY-MM-DD HH:MM:SS") DATE DATE : SDF.PARSE(STR); //3.打印结果 SYSTEM.OUT.PRINTLN(DATE.GETTIME();//1699672271000 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747450689089-b54b2161-c240-4cc9-ba90-1ebd0e8ce31f.png)



练习：（遇见不好定义的Date类的对象，先定义成字符串，在转化成新的Date类对象）

<!-- 这是一张图片，ocr 内容为：/*假设,你初恋的出生年月日为:2000-11-11 请用字符串表示这个数据,并将其转换为:2000年11月11日 创建一个DATE对象表示2000年11月11日 创建一个SIMPLEDATEFORMAT对象,并定义格式为年月日 把时间变成:2000年11月11日 /* /1.可以通过2000-11-11进行解析,解析成一个DATE对象 STRING STR - "2000-11-11"; /2.解析 SIMPLEDATEFORMAT SDF1 -NEW SIMPLEDATEFORMAT( PATTERN:"YYYY-MM-DD"); SDF1.PARSE(STR); DATE DATE //3.格式化 W SIMPLEDATEFORMAT( PATTERN:"YYY年MM月DD日"); SIMPLEDATEFORMAT SDF2 ; NEW S STRING RESULT - SDF2.FORMAT(DATE); SYST STEM.OUT.PRINTLN(RESULT); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747527902185-e3036eef-ebf1-46a4-b568-8463565b1b33.png)







<!-- 这是一张图片，ocr 内容为：1.SIMPLEDATEFORMAT的两个作用 总结 格式化 解析 2.如何指定格式 YYYY年MM月DD日HH:MM:SS -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747528503090-35ab38a3-d2d3-4de4-9162-6b9bc01031f1.png)

