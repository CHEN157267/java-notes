---
title: input语句的使用
url: https://www.yuque.com/ehsuh/iwvo3r/gl4b5te6za716abx
doc_id: 238658672
exported_at: 2026-09-12T10:33:34
---

<!-- 这是一张图片，ocr 内容为：INPUT语句(函数) 我们前面学习过PRINT语句(函数),可以完成将内容(字面量,变量等)输出到屏幕上. 在PYTHON中,与之对应的还有一个INPUT语句,用来获取键盘输入. 数据输出:PRINT 数据输入:INPUT 使用上也非常简单: 使用INPUT()语句可以从键盘获取输入 使用一个变量接收(存储)INPUT语句获取的键盘输入数据即可 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758960162567-cc0ccff5-fd1f-47f9-bab5-054755859594.png)



用例

<!-- 这是一张图片，ocr 内容为：INPUT语句(函数) 在前面的代码中,输出"请告诉我你是谁?"的PRINT语句其实是多余的 PRINT("请告诉我你是谁?") INPUT() NAME PRINT("GET!!!你是:%S"% NAME) 十 INPUT()语句其实是可以在要求使用者输入内容前,输出提示内容的哦,方式如下: ("请告诉我你是谁? NAME INPUT("请 PRINT("GET!!你是:你是:'%NAME) TEST(1) D:\DEV\PYTHON\PYTHON3.10.4\PY 请告诉我你是谁?黑马程序员 GET!!你是:黑马程序员 如图,在INPUT的括号内直接填入提示内容即可. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758960185526-b3251c1c-6ee4-4701-bd91-5fd040016603.png)



注意点：无论输入什么，都会被转化成字符串

<!-- 这是一张图片，ocr 内容为：演示PYTHON的INPUT语句 获取键盘的输入信息 INPUT("请告诉我你是谁?") 三 NAME PRINT("我知道了,你是:%S"%NAME) #输入数字类型 NUM INPUT("请告诉我你的银行卡密码:") PRINT("你的银行卡密码的类型是:",TYPE(NUM)) 它通通都把它当做字符串来看待 NTROL -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758960247801-5e0a4ece-b2fd-44d6-8567-8e2ff67062aa.png)



总结

<!-- 这是一张图片，ocr 内容为：1.INPUT()语句的功能是,获取键盘输入的数据 2.可以使用:INPUT(提示信息),用以在使用者输入内容之前显示提示 总结 信息. 3.要注意,无论键盘输入什么类型的数据,获取到的数据永远都是字 符串类型 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1758960301775-d6beaa76-2ab1-433e-b100-ae1abf65946e.png)

