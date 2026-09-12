---
title: DDL
url: https://www.yuque.com/ehsuh/oguki0/gu8zy5fgrh3kt2gk
doc_id: 213955089
exported_at: 2026-09-12T10:06:59
---

DDL的操作

1，数据库操作

<!-- 这是一张图片，ocr 内容为：DDL-数据库操作 查询 查询所有数据库 SHOW DATABASES; 查询当前数据库 SELECT DATABASE(); 创建 CREATE DATABASE[IFNOTEXISTS]数据萍名[DEFAULT CHARSET字符集][COLLATE 排序规则]; 删除 DROP DATABASE[IF EXISTS]数据库名; 使用 USE数据库名; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004193006-585332c8-f084-4df3-ae75-f044a5827d85.png)



2，表操作

（1）查询

<!-- 这是一张图片，ocr 内容为：DDL-表操作-查询 查询当前数据库所有表 SHOW TABLES; 查询表结构 DESC表名; 查询指定表的建表语句 SHOW CREATE TABLE表名; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004215212-9c123e08-873a-4491-9d2e-f3fab19d6057.png)

（2）修改

<!-- 这是一张图片，ocr 内容为：DDL-表操作-修改 添加字段 ALTER TABLE表名 ADD 字段名类型(长度)[COMMENT 注释][约束]; 案例: 为EMP表增加一个新的字段"昵称"为NICKNAME,类型为VARCHAR(20) ALTER TABLE EMP ADD NICKNAME VARCHAR(2O) COMMENT'昵称,; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004400054-3557a29b-63c0-4fa4-aef2-650aaf38549a.png)<!-- 这是一张图片，ocr 内容为：DDL-表操作-修改 修改数据类型 ALTER TABLE表名MODIFY 字段名 新数据类型(长度); 修改字段名和字段类型 ALTERTABLE表名CHANGE 旧字段名 新字段名类型(长度)[COMMENT注释][约束]; 案例: 将EMP表的NICKNAME字段修改为USERNAME,类型为VARCHAR(30) ALTER TABLE EMP CHANGE NICKNAME USERNAME VARCHAR(30) COMMENT'昵称"; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004559296-13202ace-4ef8-4dfc-a361-b0724c2d06de.png)

modify是修改指定字段的数据类型

<!-- 这是一张图片，ocr 内容为：DDL-表操作-修改 删除字段 ALTER TABLE表名 DROP 字段名; 案例: 将EMP表的字段USERNAME删除 ALTER TABLE EMP DROP USERNAME; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004491509-2be68a7c-15c8-450f-8fe9-38db877dbc42.png)

<!-- 这是一张图片，ocr 内容为：DDL-表操作-修改 修改表名 ALTER TABLE表名 RENAME TO 新表名; 案例: 将EMP表的表名修改为EMPLOYEE ALTER TABLE EMP RENAME TO EMPLOYEE; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004628250-cafb5f95-f9a2-4f2b-89ab-88fba595f788.png)

（3）创建

<!-- 这是一张图片，ocr 内容为：DDL-表操作-创建 CREATETABLE表名( 字段1字段1类型[COMMENT 字段1注释], 字段2 字段2类型[COMMENT 字段2注释], 字段3 字段3类型[COMMENT 字段3注释]. 字段N 字段N类型[COMMENT 字段N注释] ][COMMENT表注释]; 注意:[..]为可选参数,最后一个字段后面没有逗号 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004241601-ff84e309-69af-4978-8b0b-dfb72208baf6.png)



总结

<!-- 这是一张图片，ocr 内容为：1.DDL-数据库操作 SHOW DATABASES; CREATE DATABASE 数据库名; USE 数据库名; SELECT  DATABASE(); DROP  DATABASE 数据库名; 2.DDL-表操作 SHOW TABLES; CREATE.TABLE表名(字段类型,字段类型,字段类型); DESC表名; SHOW CREATE TABLE表名; ALTER TABLE 表名 ADD/MODIFY/CHANGE/DROP/RENAME TO ... DROP  TABLE表名; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1742004673508-2bb97f37-4846-4d3d-ba6a-a93a73e414bd.png)



