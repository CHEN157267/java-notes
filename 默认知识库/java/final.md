---
title: final
url: https://www.yuque.com/ehsuh/oguki0/cymvwoiy8hn83zph
doc_id: 215108897
exported_at: 2026-09-12T10:07:59
---

<!-- 这是一张图片，ocr 内容为：方法 表明该方法是最终方法,不能被重写 类 表明该类是最终类,不能被继承 变量 叫做常量,只能被赋值一次 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744505766303-14a36046-83a6-4dda-adc3-9022a797f1d7.png)



<!-- 这是一张图片，ocr 内容为：常量 实际开发中,常量一般作为系统的配置信息,方便维护,提高可读性. 常量的命名规范: 单个单词:全部大写 多个单词:全部大写,单词之间用下划线隔开 细节: FINAL修饰的变量是基本类型:那么变量存储的数据值不能发生改变. FINAL修饰的变量是引用类型:那么变量存储的地址值不能发生改变,对象内部的可以改变 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744506094309-aaa41f59-093f-40fc-8a9c-c7573fa89ac2.png)



例

<!-- 这是一张图片，ocr 内容为：//创建对象 NEW STUDENT( NAME:"ZHANGSAN", AGE:23); FINAL STUDENT TS 三 //记录的地址值不能发生改变,内部的属性值还是可以改变的 //S ; NEW STUDENT(); S.SETNAME("李四"); S.SETAGE(24); SYSTEM.OUT.PRINTLN(S.GETNAME() + ", " + S.GETAGE()); //数组 FINAL INT[] ARR {1,2,3,4,5}; INT[10]; ARR 三NEW I ARR[0]10; ARR[1]20; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744506334717-9720b1ff-fd08-4c69-b219-1a2133a49290.png)





利用final定义常量提高switch语句的阅读性（类似于C的宏常量）

<!-- 这是一张图片，ocr 内容为：PRIVATE STATIC FINAL STRING ADD STUDENR "1"; FINAL STRING DELETE_STUDENT ; "2"; PRIVATE STATIC FINAL STRING UPDATE STUDENT STATIC PRIVATE FINAL STRING QUERY_STUDENTE4": STATIC PRIVATE PUBLIC STATIC VOID STARTSTUDENTSYSTEM(){ ARRAYLIST<STUDENT> LIST ; NEW ARRAYLIST<>(); LOOP: WHILE (TRUE){ -------欢迎来到黑马学生管理系统 SYSTEM.OUT.PRINTLN("------ SYSTEM.OUT.PRINTLN("1:添加学生"); SYSTEM.OUT.PRINTLN("2:删除学生"); SYSTEM.OUT.PRINTLN("3:修改学生"); SYSTEM.OUT.PRINTLN("4:查询学生"); SYSTEM.OUT.PRINTLN("5:退出"); SYSTEM.OUT.PRINTLN("请输入您的选择:"); R SC ; NEW SCANNER(SYSTEM.IN); SCANNER S STRING CHOOSE SC.NEXT(); SWITCH (CHOOSE) CASE ADD_STUDENR -> ADDSTUDENT(LIST); DELETE_STUDENT -> DELETESTUDENT(LIST); CASE UPDATE STUDENT -> UPDATESTUDENT(LIST); CASE "4" -> QUERYSTUDENT(LIST); CASE 小八 "5" CASE SYSTEM.OUT.PRINTLN("退出"); //BREAK LOOP; SYSTEM.EXIT(STATUS:0);//停止虚拟机运行 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1744507043002-0bef7848-6f3f-4ab1-8cc3-274b51b58218.png)

