---
title: Java中对象的内存分配
url: https://www.yuque.com/ehsuh/oguki0/re3rh0q7sd91mfka
doc_id: 268089709
exported_at: 2026-09-12T10:02:38
---

<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用更短时间,教会更实用的技术! WWW.ITHEIMA.COM 内存地址 内存地址:内存中每一个小格子的编号 作用:快速的管理内存空间 64位系统:以64位的二进制表示 阅读弊端:二进制太长,转为十六进制 LILIBIH 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1777630093134-9f14feee-241f-4879-a29c-698f50e267d7.jpeg)<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用更短时间,教会更实用的技术! WWW.ITHEIMA.COM JAVA中对象的内存分配 0X0011 STRING NAME MEMORY. JAVA "小诗诗" INT AGE PUBLIC CLASS MEMORY 23 PUBLIC STATIC VOID MAIN(STRING[] ARGS){ STUDENT STU - NEW STUDENT(); 成员方法的地址 SOUT(STU); STUDY SOUT(STU.NAME + "..." + STU.AGE); STU.NAME "小诗诗"; 堆内存 MAIN 23 STU.AGE + "+ "+ STU.AGE); SOUT(STU.NAME STUDENT STU MEMORY.CLASS MAIN STU.STUDY(); 0X0011 STUDENT.CLASS NAME STUDY() AGE 栈内存 方法区 BILIB出 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1777630153845-4d251a8e-4024-48e9-a8aa-4213174cc757.jpeg)<!-- 这是一张图片，ocr 内容为：黑马程序员 多一句没有,少一句不行,用更短时间,教会更实用的技术! WWW.ITHEIMA.COM 1.STUDENTSTUDENT();创建对象的七步:创建对象的七步: 加载CLASS字节码文件 申明等号左边的局部变量 在堆里面开辟一个空间(对象) 给对象中的属性进行默认初始化 思考 给对象中的属性进行显示初始化 给对象中的属性利用构造方法进行初识化 把对象的内存地址赋值给等号左边的变量 2.方法出栈之后,方法里面的变量全部消失 3.如果没有任何地方使用堆里面的对象,那么对象也会从堆里面消失 方法区里面字节码信息一般不会消失,除非关闭虚拟机 6116出 EEZ P94 13:42/1348 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2026/jpeg/52131016/1777630161707-d40914ae-e341-4e1b-83ea-f51dfae3129d.jpeg)

