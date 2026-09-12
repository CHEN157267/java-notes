---
title: GAV坐标
url: https://www.yuque.com/ehsuh/pggizs/snqz4gdafbwmm1c6
doc_id: 277108654
exported_at: 2026-09-12T09:41:16
---



这个gav其实除了是jar包名之外，还可以是本地仓库，私服，远层仓库的文件夹的位置<!-- 这是一张图片，ocr 内容为：同聊天 U KING 2.3.GAV坐标 吓我一 大纲 NAVEN中使用三个标签来唯一定位AR资源.项目的唯一名称,创建项目时定义GAV名称,引用项目时使用93V名称,相当于项目 1.什么是MAVEN WAR和JA 的身份证号. 2.MAVEN的核心概念 2.1.POM GROUPID:组织名称,一般是公司域名的倒写 陈国庆 2.2.MAVEN工程约 ARTIFACTID:项目名称 不会 2.3.GAV坐标 3.VERSION:版本号 陈国庆 2.4.仓库 PROPER A.1.0-SNAPSHOT (开发时的临时版本号) 2.5.依赖 B.5.2.5.RELEASE(发布版本) 发送至盘会议 2.6.生命周期与插件 请输入消息... 3.MAVEN命令 定义项目 4.MAVEN的使用 5.MAVEN的依赖管理 <GROUPID>COM.JKWEILAI</GROUPID> 通过这个来定位一个甲包 6.MAVEN的继承和聚合 2 <ARTIFACTID>MAVEN_PROJECT</ARTIFACTID> 3 <VERSION>1.0.0</VERSION> 7.MAVEN私服 用项目 <DEPENDENCY> <GROUPRD>COM.IKWEILAI</GROUPID> -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1783653079748-536fd521-b4ac-4892-87d1-34f0729bbb0d.jpeg)GAV 其实是 Maven 的**全局身份证**，它定的是**三层位置**：

g是公司名反写，a是项目名，v是版本号，说是用来定位jar包位置的



project/

├── pom.xml          ← GAV 就写在这

└── src/

    ├── main/

    │   ├── java/        ← 你的业务代码

    │   └── resource/    ← 配置文件根目录！！

    └── test/

        ├── java/        ← 测试代码（@Test 那种）

        └── resource/    ← 测试用的配置文件



```java
<dependencies>
    <!-- 第一个依赖：MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.33</version>
    </dependency>

    <!-- 第二个依赖：MyBatis -->
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>3.0.3</version>
    </dependency>
    
    ... 其他依赖都往这里面扔 ...
</dependencies>
```

pom.xml中的gav用dependency双标签包裹

