---
title: DQL
url: https://www.yuque.com/ehsuh/qw2glf/kkw66z1v2u17kxx5
doc_id: 213955083
exported_at: 2026-09-12T10:34:28
---

DQL语法

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1743122185755-73fdec01-979a-4ab9-a4af-a19f62e36d9c.jpeg)



聚合函数

聚合函数都是作用于某一列的

count是计算个数，sum是计算所查的数的总和



（1)基本查询

<!-- 这是一张图片，ocr 内容为：1.查询多个字段 SELECT 字段1,字段2,字段3...FROM 表名; SELECT*FROM表名; 2. 设置别名 SELECT 字段1 [AS 别名1]字段2[AS 别名2]...FROM表名; 去除重复记录 3. 字段列表FROM表名; SELECT  DISTINCT -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744420254184-de8822cd-b905-4a60-b181-93b763e01967.png)

用例

<!-- 这是一张图片，ocr 内容为：工作地址 SELECT WORKADDRESS AS FROM EMP; 作地址 FROM SELECT WORKADDRESS 查询公司员(的上班地址(不要重复) SELECT DISTINCT WORKADDRESS '工作地址' FROM EMP; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744420299778-2318c290-0d83-4340-a581-d437f4e12452.png)



（2）条件查询

<!-- 这是一张图片，ocr 内容为：DQL-条件查询 1. 语法 条件列表; 表名 SELECT字段列表FROM WHERE 条件 功能 比较运算符 功能 逻辑运算符 并且(多个条件同时成立) AND 或 & 大于 大于等于 或者(多个条件任意一个成立) OR 或 V 小于 非(不是 NOT或! 小于等于 等于 不等于 或! 在某个范围之内(含最小,最大值) BETWEEN....AND 在IN之后的列表中的值,多选一 IN(...) 模糊匹配(匹配单个字符,%匹配任意个字符) LIKE  占位符 是NULL IS NULL -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744420696662-43200761-ef3e-4b9b-a119-a29e8ac0a840.png)



用例（主要注意 is null和not的应用）

<!-- 这是一张图片，ocr 内容为：20 FROM EMP WHERE AGE <  28 SELECT X FRO 4,直询没有身份证号的员工信息 SELECT*FROM EMP WHERE IDCARD IS NULL; 5,查询有身份证号的员工信息 NULL FROM EMP WHERE IDCARD IS NOT 大于 SELECT -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744420815205-30d978aa-fe95-4d07-95c4-c8dbcc125b99.png)

<!-- 这是一张图片，ocr 内容为：9.查询年龄等于18或20或40的员工信息 SELECT * FROM EMP WHERE AGE 18 OR AGE - 20 OR AGE -40; EMP WHERE AGE IN(18,20,40); SELECT*FROM 10,查询姓名为两个宇的员工信息 % SELECT*FROMEMPYIHERE NAME LIKE 11,查询身份证号最后一位是X的员工信息 SELECT*FROMEMP WHERE IDCARD LIKE %X -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744420841214-868d8dbb-8acb-4345-8628-ff09ee17233c.png)

在使用like时，需要用到单引号

所有的null是都不参与计算的



（3）分组查询

<!-- 这是一张图片，ocr 内容为：DQL-分组查询 1.  语法 [SELECT 字段列表 FROM 表名[WHERE 条件]GROUP BY 分组字段名[HAMNG 分组后过滤条件]; WHERE与HAVING区别 执行时机不同:WHERE是分组之前进行过滤,不满足WHERE条件,不参与分组;而HAVING是分组之后对结果进行过滤 判断条件不同:WHERE不能对聚合函数进行判断,而HAVING可以. 注意 执行顺序:WHERE>聚合函数>HAVING. 分组之后,查询的字段一般为聚合函数和分组字段,查询其他字段无任何意义. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744421251047-f5b257c8-0868-4dbc-b500-7cf20c507d1c.png)



这个其实就是先通过from后面的语句得到相应的数据，然后再通过group by将刚刚得到的数据进行分组，最后再执行前面的select的语句对每一组的数据都做那样的处理，最后将分组后的数据展示出来

用例

<!-- 这是一张图片，ocr 内容为：了.查询年龄小于45的员工,并根据工作地址分组,获取员工数量大于等于3的工作地址 >二 3; T WORKADDRESS, COUNT(*) FROM EMP WHERE AGE < 45 GROUP BY WORKADDRESS HAVING COUNT SELECT WORK -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744421621451-f22cef85-d5f0-4130-ae52-9de81d6c96c4.png)



（4）排序查询

<!-- 这是一张图片，ocr 内容为：DQL-排序查询 语法 表名ORDER BY字段1排序方式1,字段2排序方式2; SELECT字段列表FROM 排序方式 ASC:升序(默认值) DESC:降序 注意:如果是多字段排序,当第一个字段值相同时,才会根据第二个字段进行排序. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744421885308-6c845953-7835-4278-ad91-cfe8cef2e99b.png)



（5）分页查询

<!-- 这是一张图片，ocr 内容为：DQL-分页查询 语法 LIMIT起始索引,查询记录数; 表名 SELECT字段列表 FROM 注意 起始索引从0开始,起始索引:(查询页码-1)*每页显示记录数. 分页查询是数据库的方言,不同的数据库有不同的实现,MYSQL中是LIMIT. 如果查询的是第一页数据,起始索引可以省略,直接简写为LIMIT10. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744422313714-573e111c-7faf-4bed-846f-4a443fe25e06.png)



limit只能写在最后

   

（一）DQL的编写顺序

<!-- 这是一张图片，ocr 内容为：SELECT 字段列表 FROM 表名列表 WHERE 条件列表 GROUP BY 分组字段列表 HAVING 分组后条件列表 ORDER BY 排序字段列表 LIMIT 分页参数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744423398071-435a6dfd-621e-4813-9188-a6e437e168cd.png)



（二） DQL的执行顺序

<!-- 这是一张图片，ocr 内容为：FROM 表名列表 WHERE 条件列表 BY GROUP 分组字段列表 HAVING 分组后条件列表 SELECT 字段列表 ORDER BY 排序字段列表 LIMIT 分页参数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744423340846-19c73edc-c9d3-4bbc-8f31-fa069f6c5f9c.png)



<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1743122053071-ea7f844a-07db-439b-b7e2-6e73207e9b01.jpeg)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1743122053908-e52022ea-ceb3-4ddf-a8d7-610b841b37d6.jpeg)







DQL语句总结

<!-- 这是一张图片，ocr 内容为：1.DQL语句 SELECT 字段名[AS]别名 字段列表 FROM 表名 WHERE LIKE BETWEEN...AND IN VIVIANMM 条件列表 AND OR GROUP BY 分组字段列表 分组之前过滤 HAVING 分组之后过滤 分组后条件列表 ORDER BY 排序字段列表 升序ASC,降序DESC LIMIT 起始索引(从0开始),每页展示记录数 分页参数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744424571471-093623db-bc27-4c40-a54e-b9076ee49a96.png)





多表查询

```sql
-- 查询订单信息（关联 orders 和 customers 表）
SELECT orders.order_id, customers.name, orders.order_date 
FROM orders
JOIN customers 
ON orders.customer_id = customers.customer_id;

```





注：sql语言必须先排序，再分组



