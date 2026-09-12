---
title: Calender 日历类
url: https://www.yuque.com/ehsuh/oguki0/xckw65me9mlvahnf
doc_id: 219970662
exported_at: 2026-09-12T09:39:53
---

Calender本身是一个抽象类，不能直接创建对象



<!-- 这是一张图片，ocr 内容为：获取CALENDAR日历类对象的方法 说明 方法名 获取当前时间的日历对象 PUBLIC STATIC CALENDAR TANCE( GETINSTA -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747528852415-4c997be0-9bf4-4ff6-b1e6-e7a40a2441dc.png)





<!-- 这是一张图片，ocr 内容为：CALENDAR常用方法 方法名 说明 获取日期对象 PUBLIC FINAL DATE GETTIME() 给日历设置日期对象 PUBLIC FINAL SETTIME(DATE DATE) PUBLIC LONG GETTIMEINMILLIS() 拿到时间毫秒值 给日历设置时间毫秒值 PUBLIC VOID SETTIMEINMILLIS(LONG MILLIS) 取日历中的某个字段信息 PUBLIC INT GET(INT FIELD) 修改日历的某个字段信息 SET(INT FIELD,INT VALUE) PUBLIC VOID 为某个字段增加/减少指定的值 PUBLIC VOID ADD(INT FIELD,INT AMOUNT) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747529268129-6bb61b53-46fa-4459-9662-b9e65f196d24.png)





<!-- 这是一张图片，ocr 内容为：//月份:范围0~11 如果获取出来的是0.那么实际上是1月. 1/星期:在老外的眼里,星期日是一周中的第一天 7(星期六) 5(星期四) 4(星期三) 1) 1(星期日) CALENDAR C ; CALENDAR.GETINSTANCE(); 1/2.修改一下日历代表的时间 DATE D : NEW DATE(0L); C.SETTIME(D); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747530857955-d21e3db8-b5c5-4bff-805b-3000549b6c28.png)



<!-- 这是一张图片，ocr 内容为：1/调用方法在这个基础上增加一个月 -11); C.ADD(CALENDAR.MONTH,AMOUNT: -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747531454575-88caf733-a949-43fb-9c11-4bd4cedc80ad.png)

正数往后加，负数往后减





<!-- 这是一张图片，ocr 内容为：53 C.SET(CALENDAR.YEAR,2000) C.SET(CALENDAR.MONTH,999) 54 55 56 57 58 59 60 //JAVA在CALENDAR类中,把索引 61 A06 CALENDARDEMO1 F:/DEVELOPLJDK\BIN\JAVA.EXE -JAVAAGENT:F:\DEVELOP\IDEA\INTELLI JAVA.UTIL.GREGORIANCALENDAR[TIME:O,AREFIELDSSET:TRUE,AREALLFIG 2083,4,1,星期四 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747531337181-e2658fbf-45a2-4658-9746-7f4565f1e39b.png)









<!-- 这是一张图片，ocr 内容为：/JAVA在CALENDAR类中,把索引对应的数字都定义成常量 INT YEAR C.GET(CALENDAR.YEAR); INT MONTH ; C.GET(CALENDAR.MONTH) + 1; INT DATE C.GET(CALENDAR.DAY_OF_MONTH); INT WEEK C.GET(CALENDAR.DAY_OF_WEEK); SYSTEM.OUT.PRINTLN(YEAR+","+MONTH DATE GETWEEK(WEEK));/1970,1,1,1,星期四 1/查表法: //表:容器 //让数据跟索引产生对应的关系 //传入对应的数字:1~7 //返回对应的星期 PUBLIC STATIC STRING GETWEEK(INT INDEX){ 1/定义一个数组,让汉字星期几 跟1~7产生对应关系 STRING[]ARR三","星期目","星期二","星期二","星期三","星期四","星期六","星期六","星期六","星期六}; //根据索引返回对应的星期 RETURN ARR[INDEX]; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747531005007-22ce0b67-fd3a-496e-b59d-45a0ea44ad3d.png)





总结：

<!-- 这是一张图片，ocr 内容为：CALENDAR表示什么? 表示一个时间的日历对象 2.如何获取对象 通过GETINSTANCE方法获取对象 3.常见方法: 修改 SETXXX: GETXXX:获取 ADD:在原有的基础上进行增加或者减少 4.细节点: 日历类中月份的范围:0~11 日历类中星期的特点:星期日是一周中的第一天 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747531534123-f6dbf576-e598-416d-bca2-d2200dc97121.png)

