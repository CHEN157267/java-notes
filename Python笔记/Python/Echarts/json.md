---
title: json
url: https://www.yuque.com/ehsuh/iwvo3r/iuxxsqiiunsyegdx
doc_id: 245418693
exported_at: 2026-09-12T10:33:25
---

json就是不同编程语言中相互转化的中间通用语言，形式为字典或列表

<!-- 这是一张图片，ocr 内容为：JSON格式的数据要求很严格,下面我们看一下他的要求 #JSON数据的格式可以是: {"NAME"ADMIN""AGE":18] #也可以是: ["NAME":"ADMIN""AGE":18),"NAME"."ROOT""AGE":16),"NAME":20H -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1763552531392-ea7b9e98-e2ce-4ba2-967f-c1a8297158d7.png)



Python数据和Json数据的相互转化

```python
# 导入json模块
import json
# 准备符合格式json格式要求的python数据
data = [{"name":"老王","age": 16},{"name":"张三","age": 20}]
# 通过 json.dumps(data)方法把python数据转化为了 json数据
data=json.dumps(data)
# 通过 json.loads(data)方法把json数据转化为了 python数据
data=json.loads(data)
```



例子

```python
import json
#准备列表，列表内每一个元素都是字典，将其转换为JSON
data = [{"name":"张大山"，"age": 11},{"name":"王大锤"，"age": 13},{"name":"赵小虎"，"age": 16}]
json_str =json.dumps(data,ensure_ascii=False)
print(type(json_str))
print(json_str)
#准备字典，将字典转换为JSON
#将JSON字符串转换为Python数据类型[lk:V，k:v}，ik:V，k:v}]
```

#ensure_ascii=False表明我不使用ASCIl来去转换它



总结：

1.json:是一种轻量级的数据交互格式,采用完全独立于编程语言的文本格式来存储和表示数据(就是字符串)

Python语言使用JSON有很大优势，因为:JSON无非就是一个单独的字典或一个内部元素都是字典的列表

所以JSON可以直接和Python的字典或列表进行无缝转换。

2.json格式数据转化

通过 json.dumps(data)方法把python数据转化为了 json数据

data= json.dumps(data)如果有中文可以带上:ensure ascii=False参数来确保中文正常转换通过json.loads(data)方法把josn数据转化为了python列表或字典

data= json.loads(data)

