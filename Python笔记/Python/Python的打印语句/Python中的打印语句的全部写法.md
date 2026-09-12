---
title: Python中的打印语句的全部写法
url: https://www.yuque.com/ehsuh/iwvo3r/ct2ft05o05f7stg5
doc_id: 242157512
exported_at: 2026-09-12T10:34:12
---

| 方法类别 | 前缀/标志 | 基本语法示例 | 输出示例 | 简要说明 |
| --- | --- | --- | --- | --- |
| f-string (推荐) |  f  或  F  |  f"Hello, {name}"  |  Hello, Alice  | 在字符串前加  f / F ，变量/表达式直接放在  {}  内34。 |
| % 格式化 |  %  |  "Name: %s" % name  |  Name: Alice  | 类似 C 语言  printf ，使用  %s ,  %d  等作为占位符68。 |
| str.format() | 无 |  "Name: {}".format(name)  |  Name: Alice  | 使用  {}  作为占位符，通过  .format()  方法传入值16。 |




f-string (格式化字符串字面量)

```plain
# 基础变量嵌入
name = "Alice"
age = 30
print(f"My name is {name} and I am {age} years old.")

# 支持表达式和函数调用
a, b = 5, 3
print(f"{a} + {b} = {a + b}")  # 输出：5 + 3 = 8
print(f"Name in uppercase: {name.upper()}")  # 输出：Name in uppercase: ALICE

# 高级格式化：控制数字精度、对齐方式等
pi = 3.1415926
price = 99.9
print(f"Pi to 2 decimals: {pi:.2f}")  # 输出：Pi to 2 decimals: 3.14
print(f"Price: ${price:>10.2f}")  # 输出：Price: $     99.90 (宽度10,右对齐)

```



% 格式化 (旧式)

```plain
name = "Bob"
age = 25
height = 1.8765

# 单个变量
print("Hello, %s" % name)  # 输出：Hello, Bob

# 多个变量，需要用元组传入
print("Name: %s, Age: %d, Height: %.2f" % (name, age, height))
# 输出：Name: Bob, Age: 25, Height: 1.88

```



str.format() 方法

```plain
name = "Charlie"
score = 95.5

# 按顺序传入参数
print("Hello, {}! Your score is {}.".format(name, score))

# 按索引传入参数（可重复使用）
print("{1} scored {0}. Yes, {0} points!".format(score, name))

# 通过关键字参数传入
print("Player: {pname}, Score: {pscore}".format(pname=name, pscore=score))

```

