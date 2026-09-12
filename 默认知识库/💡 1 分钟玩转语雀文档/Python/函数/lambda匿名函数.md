---
title: lambda匿名函数
url: https://www.yuque.com/ehsuh/oguki0/ye15rt3485wtgzgf
doc_id: 244330257
exported_at: 2026-09-12T09:38:44
---

定义格式

lambda 传入参数:函数体(一行代码)



<!-- 这是一张图片，ocr 内容为：函数的定义中 DEF关键字,可以定义带有名称的函数 LAMBDA关键字,可以定义匿名函数(无名称) 有名称的函数,可以基于名称重复使用. 无名称的匿名函数,只可临时使用一次. 匿名函数定义语法: LAMBDA 传入参数:函数体(一行代码) LAMBDA是关键字,表示定义匿名函数 传入参数表示匿名函数的形式参数,如:X,Y表示接收2个形式参数 函数体,就是函数的执行逻辑,要注意:只能写一行,无法写多行代码 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762859437002-2cc4e0d8-73e3-461b-b489-6451893fc605.png)



```python
def test func(compute):
    result =compute(1，2)
    print(result) 
test_func(lambda x,y:x + y） #结果:3

          #效果与正常书写完全相同
def test_func(compute):
    result=compute(1，2)
    print(result)
def compute(x， y):
    return x + y
test_func(compute)

```



<!-- 这是一张图片，ocr 内容为：1.匿名函数使用LAMBDA关键字进行定义 2.定义语法: LAMBDA传入参数:函数体(一行代码) 3.注意事项: 匿名函数用于临时构建一个函数,只用一次的场景 匿名函数的定义中,函数体只能写一行代码,如果函数体要写多行 代码,不可用LAMBDA匿名函数,应使用DEF定义带名函数 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762859642032-f5829b4b-2217-4239-b7eb-c34bf9c93060.png)

