---
title: range语句的使用
url: https://www.yuque.com/ehsuh/oguki0/hg97f7q52lbgr3k9
doc_id: 238661232
exported_at: 2026-09-12T09:38:43
---

_**range只能接受整数参数**_

_**包头不包尾**_

<!-- 这是一张图片，ocr 内容为：RANGE语句 FOR循环语句,本质上是遍历:序列类型. 尽管除字符串外,其它的序列类型目前没学习到,但是不妨得我们通过学习RANGE语句,获得一个简单的数字序列, 语法1: RANGE(NUM) 获取一个从0开始,到NUM结束的数字序列(不含NUM本身) 如RANGE(5)取得的数据是:[0,1,2,3,4] -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758962138932-80916fac-7533-4070-9daa-8b6e0d97d46a.png)<!-- 这是一张图片，ocr 内容为：语法2: RANGE(NUM1, NUM2) 获得一个从NUM1开始,到NUM2结束的数字序列(不含NUM2本身) 如,RANGE(5,10)取得的数据是:[5,6,7,8,9] 语法3: RANGE(NUM1,NUM2,STEP) 获得一个从NUM1开始,到NUM2结束的数字序列(不含NUM2本身) 数字之间的步长,以STEP为准(STEP默认为1) 如,RANGE(5,10-2取得的数据是:[5,7.9] -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758962151816-154a03a6-6c07-4274-b2da-057c49ca18ae.png)



一般使用场景

```java
for i in range(数据):
```



总结

<!-- 这是一张图片，ocr 内容为：10X877 1.RANGE语句的功能是: 获得一个数字序列 2.RANGE语句的语法格式: 语法1: RANGE(NUM) 语法2 RANGE(NUM1,NUM2) 语法3: RANGE(NUM1,NUM2,STEP) 3.RANGE语句的注意事项: 语法1从0开始,到NUM结束(不含NUM本身) 语法2从NUM1开始,到NUM2结束(不含NUM2本身) 语法3从NUM1开始,到NUM2结束(不含NUM2本身) 步长以STEP值为准 RANGE的用途很多,多数用在FOR循环场景 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758962189565-ce40d3a3-5019-46fb-ae5c-03567adf844a.png)

