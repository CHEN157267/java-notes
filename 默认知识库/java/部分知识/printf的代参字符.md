---
title: printf的代参字符
url: https://www.yuque.com/ehsuh/oguki0/rmz8ogd9gcf7vx4x
doc_id: 220213328
exported_at: 2026-09-12T09:40:40
---

转换符	类型	示例	说明

 %d 	十进制整数	 

 %f 	十进制浮点数	 printf("%.2f", 3.1415)  →  3.14 	默认保留 6 位小数，可指定精度（如  %5.2f  表示总宽度 5，小数位 2）15 。

 %s 	字符串	 printf("%s", "Hello")  →  Hello 	支持宽度控制（如  %10s  右对齐， %-10s  左对齐）18 。

 %c 	单个字符	 printf("%c", 'A')  →  A 	支持 ASCII 码转换，如  char c = 65; printf("%c", c)  →  A 16 。

 %x / %X 	十六进制整数（小写/大写）	 printf("%x", 255)  →  ff 	添加  #  标志可输出前缀（如  %#x  →  0xff ）14 。

 %o 	八进制整数	 printf("%o", 64)  →  100 	类似十六进制， %#o  可加前缀  0 16 。

 %e / %E 	科学计数法浮点数	 printf("%e", 1000.0)  →  1.000000e+03 	指数形式，默认保留 6 位小数16 。

 %g / %G 	自动选择最短表示	 printf("%g", 3.14)  →  3.14 	根据值大小自动选择  %f  或  %e  格式15 。

 %% 	输出百分号	 printf("%%")  →  % 	转义输出  %  符号16 。



