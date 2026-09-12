---
title: RunTime
url: https://www.yuque.com/ehsuh/oguki0/ocgi4uwl887awgpi
doc_id: 218029994
exported_at: 2026-09-12T09:40:02
---

<!-- 这是一张图片，ocr 内容为：RUNTIME 方法名 说明 当前系统的运行环境对象 RUNTIME GETRUNTIME() PUBLIC STATIC 停止虚拟机 PUBLIC VOID EXIT(INT STATUS) 获得CPU的线程数 AVAILABLEPROCESSORS PUBLICINT JVM能从系统中获取总内存大小(单位BYTE) PUBLIC LONG MAXMEMORY() JVM已经从系统中获取总内存大小(单位BYTE) PUBLIC LONG TOTALMEMORY() JVM剩余内存大小(单位BYTE) FREEMEMORY() PUBLIC LONG 运行CMD命令 PUBLIC PROCESS COMMAND) EXEC(STRING -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746239030906-174c460e-1d8b-4bbb-9b7f-e359965fa5a1.png)

System类的exit方法实际上是调用RunTime里的exit方法







（1）getRuntime   这是所有操作的基础入口，必须先调用此方法获取  Runtime  对象。





<!-- 这是一张图片，ocr 内容为：RUNTIME.GETRUNTIME().EXEC(COMMAND:"NOTEPAD"); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746239734807-f1c4ba39-40ab-45dd-95e0-1107b7014da0.png)

这个方式输入的指令是以字符串的形式输入的

<!-- 这是一张图片，ocr 内容为：//7.运行CMD命令 //SHUTDOWN:关机 //加上参数才能执行 //-S:默认在1分钟之后关机 //-S -T指定时间:指定关机时间 //-A:取消关机操作 关机并重启 //-R: -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746239852586-4b9ca062-ad5c-421e-8986-4e9de5f492d8.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1746662100730-0bec7e62-181a-4262-9679-ce0d4314fdfe.jpeg)

t后面的单位是秒

