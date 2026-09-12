---
title: ORM
url: https://www.yuque.com/ehsuh/pggizs/bff8awploan5rhpz
doc_id: 277133835
exported_at: 2026-09-12T09:41:31
---





hibernate是全自动化orm框架，只需要执行save代码就可以完全实现orm

<!-- 这是一张图片，ocr 内容为：(MYBATIS属于半自动化ORM框架.HIBERNATE属于全自动化的ORM框架.) ORM:对象关系映射 O(OBJECT):JAVA虚拟机中的JAVA对象 R(RELATIONAL):关系型数据库 M(MAPPING):将NM中的JA对象映射到数据库表中一行已录,或是将数据库表中一行记录映射成.VM中的一个JAVA对象. 编程语言层面 对象INSTANCE USER.ID-1 类 CLASS USER USER.NAME`小明 属性:ID,NAME,EMAIL USER.EMAIL-XIAOMING@EXAM "使用面向对象语法 例如:USER.SAVE* ORM 对象关系映射 "自动生成并执行SQL 例如:INSERT INTO USERS -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783668068327-1d8d51bd-94d7-4ffb-b0d9-1cc866ad95e3.png)<!-- 这是一张图片，ocr 内容为：数据库层面 USERS数据表 ID:INT NAME:VARCHAR EMAIL:VARCHAR 表记录 1,小明', XIAOMING@EXAMPLE.COM' -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783668120778-45865222-bb8c-4390-850c-43c3f964bb06.png)

mybatis是半自动的ORM框架，因为我们需要手动写sql语句，ORM是指可以自动化将java中的对象的属性转换成sql表中的数据，也可以自动化将sql表中的数据转你换成java中对象的属性

类和表对应起来，数据与对象的属性对应起来，一个对象对应着sql一张表里的一条记录

