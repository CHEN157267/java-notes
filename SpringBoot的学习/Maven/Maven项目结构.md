---
title: Maven项目结构
url: https://www.yuque.com/ehsuh/pggizs/xrh3kgrey977d4gr
doc_id: 277108120
exported_at: 2026-09-12T09:41:17
---

包含src，pom.xml,main文件夹和test文件夹，然后这两个文件夹里都有Java和resource，resource里是那些application.yml（Spring Boot 的配置文件，以后你天天见）

mapper/*.xml（MyBatis 的 SQL 文件）

static/静态资源

各种 .properties、.xml配置

的根目录，test文件夹里的代码Maven会自动测试

<!-- 这是一张图片，ocr 内容为：园 国 朝天 B S 15PX 2.2.MAVEN工程约定的目录结构 KING 吓我一 大纲 会有预先约定好的目录结构,必须要遵循的规范,所有的MAVEN项目都依照这个规范.主要的目的源码文件, 1.什么是MAVEN 测试代码,资源文件完全分开,便于项目管理和扩展. WAR和JA 2.MAVEN的核心概念 2.1.POM 陈国庆 SRC 3 2.2.MAVEN工程约 MAIN 不会 -JAVA 2.3.GAV坐标 陈国庆 5 RESOURCES 2.4.仓库 PROPER 9 TEST 2.5.依赖 7 JAVA 发送至盘会议 RE SOURCES 单元测试放在这里. 2.6.生命周期与插件 POM.XM1 请输入消息... 3.MAVEN命令 MAVEN可以自动执行单元测试... 4.MAVEN的使用 MAVEN的依赖管理 2.3GAV坐标 MAIN目录下这个JAVA下边放的是我们的JAVA源文件 MAVEN的继承和聚合 MAVEN中使用三个标签来唯 MAVEN私服 的身份证号. 1.GROUPID:组织名称,一般是公司域名的倒写 2. ARTIFACTID:项目名称 3.VERSION:版本号 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1783653047154-4263aa97-5e35-42d2-9598-7fbcfc78cef6.jpeg)



project/

├── pom.xml          ← GAV 就写在这

└── src/

    ├── main/

    │   ├── java/        ← 你的业务代码

    │   └── resource/    ← 配置文件根目录！！

    └── test/

        ├── java/        ← 测试代码（@Test 那种）

        └── resource/    ← 测试用的配置文件

