---
title: DCL
url: https://www.yuque.com/ehsuh/qw2glf/obhwy4ee3t157bdt
doc_id: 214994932
exported_at: 2026-09-12T10:34:29
---

（非开发人员不用重点掌握）



在MySQL中用户的信息，用户的权限信息都存放在系统数据库MySQL的user表中的，所以能直接访问数据库，访问数据表

<!-- 这是一张图片，ocr 内容为：DCL-管理用户 1.查询用户 USE MYSQL; FROM USER; SELECT 创建用户 '密码'; BY USER'用户名@'主机名'IDENTIFIED CREATE 3修改用户密码 '用户名"主机名"IDENTIFIED WITH MYSQL_NATIVE_PASSWORD '新密码' ALTER USER 删除用户 DROP USER'用户名@主机名'; 注意: 主机名可以使用%通配. 这类SQL开发人员操作的比较少,主要是DBA(DATABASEADMINISTRATOR数据库管理员)使用. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744425638069-5165803f-8173-4c5a-b3ec-61906c420e84.png)

在主机名处写localhost则为只能在当前主机访问，而‘%’则为任意主机

<!-- 这是一张图片，ocr 内容为：创建用户 只能够在当前主机LOCALHOST访问,密码123456; ITCAST WWWWWW ST' IDENTIFIED BY '123456'; 'ITCAST''LOCALHOST' CREATE USER MWWWWWWW 创建用户 可以在任意主机访问该数据库,密码123456 HEIMA WWWWW IDENTIFIED D BY 123456 HEIMA CREATE USER -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744425276930-f7fd0ecf-d5e0-4166-aa4d-06aced9545c4.png)



<!-- 这是一张图片，ocr 内容为：DCL-权限控制 MYSQL中定义了很多种权限,但是常用的就以下几种: 权限 所有权限 ALL,ALL PRILEGES 查询数据 SELECT 插入数据 INSERT 修改数据 UPDATE 删除数据 DELETE 修改表 ALTER 删除数据库/表/视图 DROP 创建数据库/表 CREATE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744425734292-be8bee55-e7ac-4e13-be2d-57e3479932af.png)



<!-- 这是一张图片，ocr 内容为：DCL-权限控制 1.查询权限 FOR'用户名@'主机名'; MOHS GRANTS 2授予权限 数据库名.表名TO'用户名@主机名'; 权限列表 GRANT ON 3.撤销权限 FROM'用户名@主机名 数据库名.表名 权限列表 REVOKE ON 注意: 多个权限之间,使用逗号分隔 ,授权时,数据库名和表名可以使用*进行通配,代表所有. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744426778715-17da184b-31f0-417c-aa08-0f9b412b8163.png)

例

<!-- 这是一张图片，ocr 内容为：查询权限 FOR  HEIMA'@' SHOW GRANTS MWWWWW 授予权限  ALL ON ITCAST.* TO 'HEIMA'%'; GRANT AMWWWW 撤销权限 REVOKE ALL ON ITCAST.* FROM 'HEIMA'L AL  %    WWWW -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744426309545-a9020008-d3e6-49d1-a812-021e24e969f3.png) 

