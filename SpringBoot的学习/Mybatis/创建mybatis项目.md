---
title: 创建mybatis项目
url: https://www.yuque.com/ehsuh/pggizs/gclmghm0yqmtgzm3
doc_id: 277138103
exported_at: 2026-09-12T09:41:30
---

先创建空项目，再配置jdk和maven，之后再修改pom.xml的依赖来连接数据库



<!-- 这是一张图片，ocr 内容为：7 POM.XML(MYBATIS-001-INTRODUCTION) <?XML VERSION-"1.0" ENCODING-"UTF-8"?> 2 <PROJECT XMLNS-"HTTP://MAVEN.APACHE.ORG/POM/4.0.0" 3 XMLNS:XSI三"HTTP://WWW.W3.ORG/2001/XMLSCHEMA-INSTANCE" 4 XSI:SCHEMALOCATION:"HTTP://NAVEN.APACHE.ORG/PON//// B.D HTTP://MAVEN.APACHE-ORG/XSD/MAVEN-4.0.0.XSD" S <MODELVERSION>4.0.0</MODELVERSION> 6 7 <GROUPID>COM.JKWEILAI</GROUPID> 8 <ARTIFACTID>MYBATIS-001-INTRODUCTION</ARTIFACTID> 6 <VERSION>1.0-SNAPSHOT</VERSION> :--MYBATIS程序和JDBC一样,因此不需要打WAR包,因为普通JAVA项目就可以.歌认打包方式就是JAR-7 10 11 <PACKAGING>JAR</PACKAGING> 12 <DEPENDENCIES> 13 <!--引入MYBATIS的依赖--> 14 <DEPENDENCY> 15 <GROUPID>ORG.MYBATIS</GROUPID> 16 <ARTIFACTID>MYBATIS</ARTIFACTID> 17 <VERSION>3.5.19</VERSION> 18 </DEPENDENCY> 19 <!--引入MYSQL驱动依赖--> 20 <DEPENDENCY> 21 <GROUPID>MYSQL</GROUPID> 22 <ARTIFACTID>MYSQL-CONNECTOR-JAVA</ARTIFACTID> 23 <VERSION>8.0.24</VERSION> 24 </DEPENDENCY> 25 /DEPENDENCIES> 26 -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1783669126324-7330c8c7-cd5a-41ae-9f7a-47e5b134bc27.png)

其中，<packing>jar</packing>应该是将项目打包成jar包的代码

要在依赖中，gav下加上<scope>runtime</scope>应该是确保项目运行期间，这个能正常使用



| **scope** | **编译期能用？** | **测试期能用？** | **打包运行时能用？** | **典型例子** |
| :--- | :--- | :--- | :--- | :--- |
| **compile**（默认） | ✅ | ✅ | ✅ | 大部分依赖，如 MyBatis 核心包 |
| **test** | ❌ | ✅ | ❌ | JUnit（测试才用，上线不打进去） |
| **runtime** | ❌ | ✅ | ✅ | **MySQL 驱动** |


**不写默认就是 **`**compile**`**。** 这意味着这个 jar 包在编译、测试、运行阶段都要参与。

“连接数据库的 jar 包用 runtime”

