---
title: Objects
url: https://www.yuque.com/ehsuh/oguki0/kgs7gacsger0valt
doc_id: 218107676
exported_at: 2026-09-12T09:39:57
---





Object是一个工具类，提供了一些方法去完成一些功能

<!-- 这是一张图片，ocr 内容为：说明 方法名 PUBLIC STATIC BOOLEAN EQUALS(OBJECT A,OBJECT B) 先做非空判断,比较两个对象 判断对象是否为NULL,为NULL返回TRUE,反之 PUBLIC STATIC BOOLEAN ISNULL(OBJECT OBJ) 判断对象是否为NULL,跟ISNULI的结果相反 PUBLIC STATIC BOOLEAN NONNULL(OBJECT OBJ) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746620144579-b325f296-c7ca-49f4-a1c4-d1430359f325.png)



equals方法的细节：

<!-- 这是一张图片，ocr 内容为：BOOLEAN RESULT ; OBJECTS.EQUALS(S1, S2); SYSTEM.OUT.PRINTLN(RESULT); //细节: /1.方法的底层会判断S1是否为NULL,如果为NULL,直接这回FALSE /2.如果S1不为NULL,那么就利用S1再次调用EQUALS方法 /3.此时S1是STUDENT类型,所以最终还是会调用STUDENT中的EQUALS方法. 如果没有重写,比较地址值,如果重写了,就比较属性值. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746620663340-026b5702-6a87-4444-81c6-36b03f6572f3.png)



总结：

<!-- 这是一张图片，ocr 内容为：OBJECTS是一个对象工具类,提供了一些操作对象的方法 2.EQUALS(对象1,对象2):先做非空判断,比较两个对象 3.ISNULL(对象):判断对象是否为空 4.NONNULL(对象):判断对象是否不是空 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746620845593-c39efb58-8902-4b5f-8757-e1aa0770288a.png)

