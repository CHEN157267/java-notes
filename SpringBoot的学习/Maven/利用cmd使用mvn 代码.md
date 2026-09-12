---
title: 利用cmd使用mvn 代码
url: https://www.yuque.com/ehsuh/pggizs/tttk22q5st3y61oh
doc_id: 277110464
exported_at: 2026-09-12T09:41:14
---

mvn compile（编译）

你看到的：生成了 target文件夹，里面一堆 .class字节码文件。

mvn clean（清理）

你看到的：target文件夹没了。

mvn install（安装）

你看到的：它不光编译、测试，最后还把打包好的 jar文件复制到了你配置的本地仓库（比如 D:\repository）里。





compile= 编译

clean= 清空

install= 打包并存入本地仓库

<!-- 这是一张图片，ocr 内容为：锅雨料系 面 已保存 14:01:58 分享 MAVEN&NEXUS 一园饮园 3.1.生命周期上的核心命令 有了 大纲 MAVEN有3个内置生命周期,每个生命周期包含多个阶段,用户可通过MVN<PHASE>命令触发执行. 脱 *1.什么是MAVEN 有了 3.1.1 DEFAULT 生命周期(核心构建流程) 2.MAVEN的核心 3.MAVEN命令 用途:编译,测试,打包,部署项目曾列等完合自适应完度 现在布 `3.1.生命周期 核心阶段(按顺序执行): 3.2.组合命令 3.3.特殊命令 现在有了 命令(MVN<PHASE>) 作用 3.4.重点规则 验证项目配置是否正确(如) 是否合法) VALIDATE 3.5开发工具 4.MAVEN的使用 编译项目的主代码(生成 TARGET/CLASSES 5.MAVENF门依赖 发送至主会议中所有人 运行单元测试(使用MAVEN-SUREFIRE-PLUGIN). TEST 6.MARVEN的继承 请输入消息 打包项目(生成JAR/WAR等,存放于 TARGET/ 目录). *7.MAVEN私服 运行集成测试或检查构建质量(如 MAVEN-FAILSAFE PLUGIN). 将构建的产物安装到本地仓库(默认在~/.M2/REPOSITORY). INSTA11 将构建的产物部署到远程仓库(如 NEXUS,ARTIFACTORY). DEPLOY 常用命令示例: # 执行到 COMPILE 阶段(含 VALIDATE +COMPILE) MVN COMPILE #执行到 TEST 阶段(含 VALIDATE + COMPILE + TEST) MVN TEST 执行到PACKAGE阶段(含 MVN PACKAGE 啊然后呢进行一个这个安装安装 执行到INSTALL阶段<含前) MVN INSTALL 管理货:GRMNDO.. MIUN RAPOSITOR MEVENKEAR -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1783655734617-012a10c1-ebe2-4d2c-8bbf-26a9dbeb538f.jpeg)

