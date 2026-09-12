---
title: _lt_中小于符号比较方法
url: https://www.yuque.com/ehsuh/oguki0/qyggctcnr2dlrsgc
doc_id: 246188560
exported_at: 2026-09-12T09:38:04
---

<!-- 这是一张图片，ocr 内容为：行,用最内部比较器有品发 1.6 中国电信3:40 4G. 52 K/S 马程序员 公交车二XI工门 1037X972PX 小于符号比较方法 CLASS STUDENT: DEF-INIT_(SELF,NAME,AGE): SELF.NAME - NAME TRACEBACK (MOST RECENT CALL LAST): FILE "D:\PYTHON-LEARN\TEST.PY",LINE 11, IN <MADULE> SELF.AGE - AGE PRINT(STU1< STU2) STUDENT' TYPEERROR:'<'NOT SUPPORTED BETWEEN INSTANCES OF ' STUDENT' AND'ST STU1 STUDENT("周杰轮",11) STU2  STUDENT("林军杰",13) PRINT(STU1 < STU2) 直接对2个对象进行比较是不可以的,但是在类中实现IT 方法,即可同时完成:小于符号和大于符号2种比较. CLASS STUDENT: DEF__INIT_(SELF.NAME. AGE): SELF.NAME NAME SELF.AGE AGE 方法名:____ 传入参数:OTHER,另一个类对象 DEF__1T_(SELF,OTHER): 返回值:TRUE或FALSE RETURN SELF.AGE<OTHER.AGE 内容:自行定义 STULSTUDENT("周杰轮",11) 它是用于小于符号比较的 STU2STUDENT("林军杰",13) 黑马程序员出5出 PRINT(STU1<STU2)# TRUE STU2) #结果,FALUE PRINT(STU1 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2025/jpeg/52131016/1764071236165-9afe8134-53d5-4031-853b-167167d0fb83.jpeg)



```html
#__lt__魔术方法
def -_lt__(self, other):
return self.age < other.age
```

