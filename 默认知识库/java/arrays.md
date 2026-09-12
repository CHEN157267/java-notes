---
title: arrays
url: https://www.yuque.com/ehsuh/oguki0/paig31q5x9ox9if3
doc_id: 221617688
exported_at: 2026-09-12T09:39:36
---

操作数组的工具类

<!-- 这是一张图片，ocr 内容为：ARRAYS 操作数组的工具类. 方法名 说明 把数组拼接成一个字符串 PUBLIC STATIC STRING TOSTRING(数组) 二分查找法查找元素 PUBLIC STATIC INT BINARYSEARCH(数组,查找的元素) 拷贝数组 PUBLIC STATIC INT[] COPYOF(原数组,新数组长度) PUBLIC STATIC INT[] COPYOFRANGE(原数组,起始索引,结束索引) 拷贝数组(指定范围) 填充数组 PUBLIC STATIC VOID FILL(数组,元素) PUBLIC STATIC VOID SORT(数组) 按照默认方式进行数组排序 按照指定的规则排序 PUBLIC STATIC  VOID SORT(数组,排序规则) -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1748436837643-4dd89467-2ec9-47b1-ad78-4e6be0f4381c.jpeg)





用例及细节

<!-- 这是一张图片，ocr 内容为：//TOSTRING:将数组变成字符串 17 -------TOSTRING SYSTEM.OUT.PRINTIN("- 18 INT[] ARR 三{1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; 19 SYSTEM.OUT.PRINTIN(ARRAYS.TOSTRING(ARR));//(11, 2, 3,4,5, 6, 7, 8,9, 10) //BINARYSEARCH:二分查找法查找元素 /细节1:二分查找的前提:数组中的元素必须是有序,数组中的元素必须是升序的 25 /细节2:如果要查找的元素是存在的,那么返回的是真实的索引 //但是,如果要查找的元素是不存在的,返回的是-插入点-1 26 //疑问:为什么要减1呢? 27 /解释:如果此时,我现在要查找数字0,那么如果返回的值是一插入点,就会出现问题了. 28 /如果要查找数字0,此时0是不存在的,但是按照上面的规则一插入点,应该就是-O 29 //为了避免这样的情况,JAVA在这个基础上又减一. 30 31 SYSTEM.OUT.PRINTLN("-- -BINARYSEARCH- SYSTEM.OUT.PRINTIN(ARRAYS.BINARYSEARCH(ARR,KEY:10));//9 SYSTEM.OUT.PRINTIN(ARRAYS.BINARYSEARCH(ARR,KEY:2);//1 SYSTEM.OUT.PRINTIN(ARRAYS.BINARYSEARCH(ARR,KEY:20));//-11 35 -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1748436849356-4c414c63-8c1a-4010-ac71-e205a780d7df.jpeg)

<!-- 这是一张图片，ocr 内容为：//COPYOF:拷贝数组 1/参数一:老数组 1/参数二:新数组的长度 1/方法的底层会根据第二个参数来创建新的数组 1/如果新数组的长度是小于老数组的长度,会部分拷贝 1/如果新数组的长度是等于老数组的长度,会完全拷贝 1/如果新数组的长度是大于老数组的长度,会补上默认初始值 SYSTEM.OUT.PRINTLN("--- --------------COPYOF-- INT[]NEWARR1 ARRAYS.COPYOF(ARR,NEWLENGTH:20); SYSTEM.OUT.PRINTIN(ARRAYS.TOSTRING(NEWARR1));/////(11, 2,3,4,5, 6, 7,8, 8,9,101 //COPYOFRANGE:拷贝数组(指定范围) 1/细节:包头不包尾,包左不包右 SYSTEM.OUT.PRINTLN(" COPYOFRANGE INT[] NEWARR2- ARRAYS.COPYOFRANGE(ARR,FROM:0, TO:9); SYSTEM.OUT.PRINTLN(ARRAYS.TOSTRING(NEWARR2)); -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1748436855291-9a39d3bc-1541-4aab-8824-415bd253e9d5.jpeg)

<!-- 这是一张图片，ocr 内容为：//FILL:填充数组 FILL SYSTEM.OUT.PRINTLN("- ARRAYS.FILL(ARR,VAL:100); SYSTEM.OUT.PRINTLN(ARRAYS.TOSTRING(ARR)); 底层使用的是快速排序. /SORT:排序.默认情况下,给基本数据类型进行升序排列. SYSTEM.OUT.PRINTLN("------- -------------SORT- INT[] ARR2 {10, 2, 3, 5, 6, 1, 7, 8, 4, 9}; ARRAYS.SORT(ARR2); SYSTEM.OUT.PRINTIN(ARRAYS.TOSTRING(ARR2));////11, 2, 4, 5, 6, 7, 8, 9, 10] I -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1748436862276-cf725764-19a1-45e9-b341-e23730e0fbe2.jpeg)

