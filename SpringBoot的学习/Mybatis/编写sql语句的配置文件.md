---
title: 编写sql语句的配置文件
url: https://www.yuque.com/ehsuh/pggizs/krqld8f4d3fss45d
doc_id: 277141951
exported_at: 2026-09-12T09:41:28
---



命名方式：<!-- 这是一张图片，ocr 内容为：RESOURCES >/>CARMAPPER.XML </>MYBATIS-CONFIG.XML )TEST M POM.XML MYBATIS.IML LMAPPER. XML ERNAL LIBRARIES ATCHES AND CONSOLES 和数据库表名对应上. T_CAR CARMAPPER. XML CAR T USER USERMAPPER.XML -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783670472282-ea1d6af6-1f4d-44ce-841c-adf537207aef.png)



在mapper标签中填写sql语句，上面的dtd文件是用来控制mapper标签中能写入什么标签和标签编写顺序的约束，算是规则，也叫做约束文件

<!-- 这是一张图片，ocr 内容为：MYBATIS-CONFIG.XML CARMAPPER.XML M POM.XML(MYBATIS-001-INTRODUCTION) <?XML VERSION-"1.0" ENCODING"UTF-8" ?> <!DOCTYPE MAPPER IC "-//MYBATIS.ORG//DTD MAPPER 3.0//EN" PUBLIC "- "HTTPS://MYBATIS.ORG/DTD/MYBATIS-3-MAPPER.DTD"> 4 5 6 <MAPPER NAMESPACE:"CAR"> 7 <SELECT ID-"SELECTBLOG" RESULTTYPE:"BLOG" 8 SELECT * FROM BLOG WHERE ID - #{ID} 9 </SELECT> 10 11 </MAPPER> 12 能编写什么标签? 标签的编写顺序... -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783670627649-544fdfde-072c-4722-9525-3d79d5552b80.png)

