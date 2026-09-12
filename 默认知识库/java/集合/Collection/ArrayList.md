---
title: ArrayList
url: https://www.yuque.com/ehsuh/oguki0/cwek4p2qxhwa7kgb
doc_id: 212880556
exported_at: 2026-09-12T10:08:02
---

```plain
arraylist<string> list = new arraylist<>();
```

_**<font style="color:#DF2A3F;">//尖括号内也可以写类名</font>**_

<!-- 这是一张图片，ocr 内容为：ARRAYLIST成员方法 方法名 说明 增 BOOLEAN ADD(E E) 添加元素,返回值表示是否添加成功 BOOLEAN REMOVE(E E) 删除指定元素,返回值表示是否删除成功 删 E REMOVE(INT INDEX) 删除指定索引的元素,返回被删除元素 改 修改指定索引下的元素,返回原来的元素 E SET(INT INDEX,E E) E GET(INT INDEX) 获取指定索引的元素 查 INT SIZE() 集合的长度,也就是集合中元素的个数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743217935964-308a80bc-878a-4a80-992d-58340eae0af7.png)

```java
list.add("aaa");
boolean result1 = list.remove("aaa");
system.out.println(result1);
string result = list.set(1, "ddd");
system.out.println(result);//aaa
string s = list.get(0);
system.out.println(s);
list.size();//4
//遍历
for(int i;i < list.size(); i++) {
//1ist.get(i)  获取元素
string str = list.get(i);
system.out.println(str);
```



<!-- 这是一张图片，ocr 内容为：基本数据类型对应的包装类 BYTE BYTE SHORT SHORT CHAR CHARACTER INTEGER INT LONG LONG FLOAT FLOAT DOUBLE DOUBLE BOOLEAN BOOLEAN -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743296409588-1007fefc-0d53-4756-a1c1-3d3f86cd8665.png)



（user是一个类，含有id）

<!-- 这是一张图片，ocr 内容为：根据ID查找用户 //1.我要干嘛? 1/2.我干这件事需要什么才能完成? ID LIST //3.调用处是否需要使用方法的结果? 返回 PUBLIC STATIC BOOLEAN CONTAINS(ARRAYLIST<USER> LIST, STRING ID)( FOR (INT I ; 0; I < LIST.SIZE(); I++) { USER U ; LIST.GET(I); STRING UID - U.GETID(); IF(UID.EQUALS(ID)) //如果找到了直接返回TRUE RETURN TRUE; 子 1/当循环结束表示集合里面所有的元素都已经比较完毕,还没有一样的,那么 RETURN FALSE; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743404900780-0c32a65d-ae81-43ad-98ba-8a0a95603176.png)

或

<!-- 这是一张图片，ocr 内容为：LIST.GET(I).GETID().EQUALS(ID) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743404931702-1f467a66-ffbc-49f2-bf46-c112dcb8a325.png)



当要求需要两个相近的方法的时候，可以利用方法的调用适当减少代码

<!-- 这是一张图片，ocr 内容为：CONTAINS(ARRAYLIST<USER> LIST, STRING ID){ PUBLIC STATIC BOOLEAN /* FOR (INT I 三 0; I < LIST.SIZE(); I+){ USER U : LIST.GET(I);  STRING UID - U.GETID();  IF(UID.EQUALS(ID)){ //如果找到了直接返回TRUE RETURN TRUE; //当循环结束表示集合里面所有的元素部已经比较完毕,还没有一样的,那么运回FALSE就可以了 RETURN FALSE;*/ RETURN GETINDEX(LIST,ID) >; O; PUBLIC STATIC INT GETINDEX(ARRAYLIST<USER> LIST, STRING ID)-{ FOR (INT I - 0; I < LIST.SIZE(); I++) { USER U - LIST.GET(I); STRING UID : U.GETID(); IF(UID.EQUALS(ID)){ I; RETURN -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743405473869-5ca0ec08-9efe-4265-9498-bd5b3e7d8f30.png)









Java 自带的  contains  方法解析

1. 归属与语法

归属:  contains  是  Collection  接口（如  ArrayList 、 HashSet ）的内置方法



作用: 判断集合中是否包含指定对象  o 

```java
boolean contains(Object o)

```



```java
List<User> users = new ArrayList<>();
users.add(new User("001", "Alice"));
boolean exists = users.contains(new User("001", "Alice")); // 结果取决于 User.equals() 的实现

```

