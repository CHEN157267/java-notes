---
title: Collection
url: https://www.yuque.com/ehsuh/oguki0/ndr1pr4rba9virtf
doc_id: 222815597
exported_at: 2026-09-12T10:08:00
---

单列集合

添加数据的时候，每次只能添加一个数据



<!-- 这是一张图片，ocr 内容为：COLLECTION COLLECTION是单列集合的祖宗接口,它的功能是全部单列集合都可以继承使用的. 说明 方法名称 把给定的对象添加到当前集合中 PUBLIC BOOLEAN ADD(E E) 清空集合中所有的元素 PUBLIC VOID CLEAR() 把给定的对象在当前集合中删除 PUBLIC BOOLEAN REMOVE(E E) 判断当前集合中是否包含给定的对象 PUBLIC BOOLEAN CONTAINS(OBJECT OBJ) 判断当前集合是否为空 PUBLIC BOOLEAN ISEMPTY() 返回集合中元素的个数/集合的长度 PUBLIC INT SIZE() -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1749263118244-9a6b765e-6938-4072-a75f-3411fea0b5d5.png)



这两个方法值得注意

<!-- 这是一张图片，ocr 内容为：//3.删除 //细节1,因为COLLECTION里而定义的是共性的方法,所以此时不能通过索引进行副除.只能通过元素的对家进行副际. //细节2:方法会有一个布尔类型的这回值,删除成功这回TRUE,删除失败这回FALSE //如果要删除的元素不存在,就会删除失败. SYSTEM.OUT.PRINTLN(COLL.REMOVE(O:"AAA")); SYSTEM.OUT.PRINTLN(COLL); /4.判断元素是否包含 1/细节:底层是依赖EQUALS方法进行判断是否存在的. //所以,如果华合中存储的是自定义对家,也想通过CONTAINS方法来判断是否包含,那么在JAVABEAN类中,一定要重与EQUALS方法 BOOLEAN RESULT ; COLL.CONTAINS("BBB"); SYSTEM.OUT.PRINTLN(RESULT); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1749265042040-3c8e1188-76c2-4dd2-a69f-e8dd1ef7b44d.png)

