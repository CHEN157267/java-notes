---
title: Python和Java的书写区别
url: https://www.yuque.com/ehsuh/iwvo3r/wxb2oorrctwqkdpc
doc_id: 237592624
exported_at: 2026-09-12T10:34:13
---

Python 和 Java 在代码书写上存在显著差异，这主要源于它们不同的设计哲学。Python 追求 **简洁明了** 和 **开发效率**，而 Java 则更强调 **严谨清晰** 和 **类型安全。**

| 特性 | Python | Java |
| :--- | :--- | :--- |
| **代码块** | 缩进（通常4空格） | 大括号 `{}` |
| **语句结束** | 通常无需分号 | 必须使用分号 `;` |
| **变量类型** | 动态类型，无需声明 | 静态类型，必须声明 |
| **函数/方法** | `def`定义，无需类型声明 | 需指定返回类型和参数类型 |
| **主程序入口** | 无特定方法，脚本即执行 | `public static void main` |
| **注释** | `#`单行，`'''`或`"""`多行 | `//`单行，`/* */`多行 |
| **文档字符串** | `"""`文档字符串，运行时可访问 | `/** */`Javadoc，生成API文档 |




****

****

### 1. 🔍 变量定义
Python 是动态类型语言，变量无需声明类型，类型在运行时确定

**Python的变量声名无需声明类型**

**例：**

```python
name = "Alice"  # 字符串
age = 30        # 整数
score = 95.5    # 浮点数
is_pass = True  # 布尔值
```



### 2. 🔧 函数 vs. 方法
Python 使用 `def`关键字定义函数，无需指定参数和返回值的类型。

```python
def add(a, b):    # 无需类型声明
    return a + b

result = add(5, 3)  # 可以传递整数
result2 = add("Hello, ", "World!")  # 也可以传递字符串，连接起来
```



这是Java定义函数

```java
public class Calculator {
    public static int add(int a, int b) { // 必须声明参数和返回类型为int
        return a + b;
    }
}

int result = Calculator.add(5, 3); // 调用方法
// Calculator.add("Hello", "World"); // 这行会编译报错，类型不匹配
```



### 3. 🧱 代码块与缩进


Python 使用冒号(`:`)和**缩进**（通常4个空格）来定义代码块，缩进是语法的一部分。

_Python 依靠缩进层级区分代码块。_

```python
if age >= 18:
    print("成年")
    print("可以投票了")  # 这行也在if块内
else:
    print("未成年")
print("程序继续")  # 这行已在if-else块之外
```



Python 和 Java 在代码书写上存在显著差异，这主要源于它们不同的设计哲学。Python 追求 **简洁明了** 和 **开发效率**，而 Java 则更强调 **严谨清晰** 和 **类型安全**

。

下面是一个快速了解两者主要书写差异的表格：

| 特性 | Python | Java |
| :--- | :--- | :--- |
| **代码块** | 缩进（通常4空格） | 大括号 `{}` |
| **语句结束** | 通常无需分号 | 必须使用分号 `;` |
| **变量类型** | 动态类型，无需声明 | 静态类型，必须声明 |
| **函数/方法** | `def`定义，无需类型声明 | 需指定返回类型和参数类型 |
| **主程序入口** | 无特定方法，脚本即执行 | `public static void main` |
| **注释** | `#`单行，`'''`或`"""`多行 | `//`单行，`/* */`多行 |
| **文档字符串** | `"""`文档字符串，运行时可访问 | `/** */`Javadoc，生成API文档 |


接下来我们看一些具体的代码示例。

### 1. 🔍 变量定义
Python 是动态类型语言，变量无需声明类型，类型在运行时确定

。

```plain
name = "Alice"  # 字符串
age = 30        # 整数
score = 95.5    # 浮点数
is_pass = True  # 布尔值
```

_Python 中变量直接赋值，类型自动推断。_

Java 是静态类型语言，变量必须显式声明类型

。

```plain
String name = "Alice"; // 必须声明为String
int age = 30;          // 必须声明为int
double score = 95.5;   // 必须声明为double
boolean isPass = true; // 必须声明为boolean
```

_Java 中每个变量都必须先声明其类型。_

### 2. 🔧 函数 vs. 方法
Python 使用 `def`关键字定义函数，无需指定参数和返回值的类型

。

```plain
def add(a, b):    # 无需类型声明
    return a + b

result = add(5, 3)  # 可以传递整数
result2 = add("Hello, ", "World!")  # 也可以传递字符串，连接起来
```

_Python 函数定义灵活，但调用时需注意参数类型。_

Java 中方法（函数）必须在类中定义，需明确指定参数和返回值的类型

。

```plain
public class Calculator {
    public static int add(int a, int b) { // 必须声明参数和返回类型为int
        return a + b;
    }
}

int result = Calculator.add(5, 3); // 调用方法
// Calculator.add("Hello", "World"); // 这行会编译报错，类型不匹配
```

_Java 方法定义严格，类型安全在编译期检查。_

### 3. 🧱 代码块与缩进
Python 使用冒号(`:`)和**缩进**（通常4个空格）来定义代码块，缩进是语法的一部分

。

```plain
if age >= 18:
    print("成年")
    print("可以投票了")  # 这行也在if块内
else:
    print("未成年")
print("程序继续")  # 这行已在if-else块之外
```

_Python 依靠缩进层级区分代码块。_

__

__

Java 使用**大括号**** **`**{}**` 来定义代码块，缩进主要用于提升可读性

_Java 用花括号明确代码块边界，缩进是风格问题。_  
 

```java
if (age >= 18) {
    System.out.println("成年");
    System.out.println("可以投票了");
} else {
    System.out.println("未成年");
}
System.out.println("程序继续");
```







### 4. 🐘 面向对象
Python 定义类使用 `class`，构造方法名为 `__init__`，实例方法第一个参数通常是 `self`（代表实例本身)。

_Python 的面向对象语法更简洁。_

```python
class Person:
    def __init__(self, name, age):  # 构造方法
        self.name = name    # 实例属性
        self.age = age

    def introduce(self):    # 实例方法
        print(f"我叫{self.name}, 今年{self.age}岁。")

# 使用类
p = Person("Alice", 30)  # 创建对象，无需new关键字
p.introduce()            # 调用方法
```



Java 定义类使用 `class`，构造方法名与类名相同，使用 `this`关键字引用当前实例。

_Java 的面向对象语法更正式严谨，封装性更强_

```java
public class Person {
    private String name; // 属性通常私有
    private int age;

    public Person(String name, int age) { // 构造方法
        this.name = name;
        this.age = age;
    }

    public void introduce() {
        System.out.println("我叫" + this.name + ", 今年" + this.age + "岁。");
    }
}

// 使用类
Person p = new Person("Alice", 30); // 使用new关键字创建对象
p.introduce();
```



### 5. 💬 注释与文档
Python 使用 `#`进行单行注释，使用三引号 `'''`或 `"""`进行多行注释或作为文档字符串 (Docstring)

。

```python
# 这是一个单行注释

"""
这是一个多行注释
通常用于模块、类或函数的描述性文档
（也称为文档字符串）
"""

def calculate_sum(a, b):
    """这是一个函数的文档字符串，用于说明函数的功能和参数。
    
    Args:
        a: 第一个加数
        b: 第二个加数
        
    Returns:
        两个数的和
    """
    return a + b

# 甚至可以运行时访问文档字符串
print(calculate_sum.__doc__)
```

_Python 的文档字符串是语言特性，可用于自动生成文档或在运行时查看。_

Java 使用 `//`进行单行注释，`/* */`进行多行注释，`/** */`用于生成 Javadoc 文档

。

```java
// 这是一个单行注释

/*
这是一个多行注释
*/

/**
 * 这是一个Javadoc注释，用于生成API文档。
 * @param a 第一个加数
 * @param b 第二个加数
 * @return 两个数的和
 */
public int calculateSum(int a, int b) {
    return a + b;
}
```

_Java 的 Javadoc 注释通过工具生成离线API文档。_

### 6. 🎨 特有语法
Python 提供了一些**语法糖**让代码更简洁。

**列表推导式**：快速生成列表

+ 。

```python
squares = [x**2 for x in range(10)] # [0, 1, 4, 9, ..., 81]
```

**切片**：优雅处理序列的子集

+ 。

```python
my_list = [0, 1, 2, 3, 4, 5]
sub_list = my_list[1:4]  # [1, 2, 3]
```

**f-string**：灵活的字符串格式化（Python 3.6+）

+ 。

```python
name = "Alice"
age = 30
greeting = f"Hello, {name}. You are {age} years old."
```

Java 的语法特性更注重**类型安全**和**结构严谨**。

**泛型**：提供编译时类型检查

+ 。

```java
List<String> list = new ArrayList<>(); // 只能存放String
list.add("Hello");
// list.add(42); // 编译错误
```

**注解**：为代码添加元数据

+ 。

```java
@Override // 注解，表示方法重写
public void introduce() { ... }
```

### 💎 总结
Python 和 Java 的书写风格差异巨大，这体现了它们不同的设计哲学：

**Python** 像**“写笔记”**，**简洁灵活**，追求开发效率和表达力，适合快速原型、脚本、数据科学和AI

+ 。

**Java** 像**“写正式报告”**，**严谨清晰**，强调结构、类型安全和可维护性，适合大型企业应用、复杂后端系统和Android开发

+ 。

