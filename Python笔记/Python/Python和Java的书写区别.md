---
title: Python和Java的书写区别
url: https://www.yuque.com/ehsuh/iwvo3r/wxb2oorrctwqkdpc
doc_id: 237592624
exported_at: 2026-09-12T10:34:13
---

<font style="color:rgb(0, 0, 0);">Python 和 Java 在代码书写上存在显著差异，这主要源于它们不同的设计哲学。Python 追求 </font>**<font style="color:rgb(0, 0, 0);">简洁明了</font>**<font style="color:rgb(0, 0, 0);"> 和 </font>**<font style="color:rgb(0, 0, 0);">开发效率</font>**<font style="color:rgb(0, 0, 0);">，而 Java 则更强调 </font>**<font style="color:rgb(0, 0, 0);">严谨清晰</font>**<font style="color:rgb(0, 0, 0);"> 和 </font>**<font style="color:rgb(0, 0, 0);">类型安全。</font>**

| <font style="color:rgb(0, 0, 0);">特性</font> | <font style="color:rgb(0, 0, 0);">Python</font> | <font style="color:rgb(0, 0, 0);">Java</font> |
| :--- | :--- | :--- |
| **<font style="color:rgb(0, 0, 0);">代码块</font>** | <font style="color:rgb(0, 0, 0);">缩进（通常4空格）</font> | <font style="color:rgb(0, 0, 0);">大括号</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">{}</font>` |
| **<font style="color:rgb(0, 0, 0);">语句结束</font>** | <font style="color:rgb(0, 0, 0);">通常无需分号</font> | <font style="color:rgb(0, 0, 0);">必须使用分号</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">;</font>` |
| **<font style="color:rgb(0, 0, 0);">变量类型</font>** | <font style="color:rgb(0, 0, 0);">动态类型，无需声明</font> | <font style="color:rgb(0, 0, 0);">静态类型，必须声明</font> |
| **<font style="color:rgb(0, 0, 0);">函数/方法</font>** | `<font style="color:rgb(0, 0, 0);">def</font>`<font style="color:rgb(0, 0, 0);">定义，无需类型声明</font> | <font style="color:rgb(0, 0, 0);">需指定返回类型和参数类型</font> |
| **<font style="color:rgb(0, 0, 0);">主程序入口</font>** | <font style="color:rgb(0, 0, 0);">无特定方法，脚本即执行</font> | `<font style="color:rgb(0, 0, 0);">public static void main</font>` |
| **<font style="color:rgb(0, 0, 0);">注释</font>** | `<font style="color:rgb(0, 0, 0);">#</font>`<font style="color:rgb(0, 0, 0);">单行，</font>`<font style="color:rgb(0, 0, 0);">'''</font>`<font style="color:rgb(0, 0, 0);">或</font>`<font style="color:rgb(0, 0, 0);">"""</font>`<font style="color:rgb(0, 0, 0);">多行</font> | `<font style="color:rgb(0, 0, 0);">//</font>`<font style="color:rgb(0, 0, 0);">单行，</font>`<font style="color:rgb(0, 0, 0);">/* */</font>`<font style="color:rgb(0, 0, 0);">多行</font> |
| **<font style="color:rgb(0, 0, 0);">文档字符串</font>** | `<font style="color:rgb(0, 0, 0);">"""</font>`<font style="color:rgb(0, 0, 0);">文档字符串，运行时可访问</font> | `<font style="color:rgb(0, 0, 0);">/** */</font>`<font style="color:rgb(0, 0, 0);">Javadoc，生成API文档</font> |




**<font style="color:#DF2A3F;"></font>**

**<font style="color:#DF2A3F;"></font>**

### <font style="color:rgba(0, 0, 0, 0.9);">1. </font><font style="color:rgba(0, 0, 0, 0.9);">🔍</font><font style="color:rgba(0, 0, 0, 0.9);"> 变量定义</font>
<font style="color:rgb(0, 0, 0);">Python 是动态类型语言，变量无需声明类型，类型在运行时确定</font>

**<font style="color:#DF2A3F;">Python的变量声名无需声明类型</font>**

**<font style="color:#DF2A3F;">例：</font>**

```python
name = "Alice"  # 字符串
age = 30        # 整数
score = 95.5    # 浮点数
is_pass = True  # 布尔值
```



### <font style="color:rgba(0, 0, 0, 0.9);">2. </font><font style="color:rgba(0, 0, 0, 0.9);">🔧</font><font style="color:rgba(0, 0, 0, 0.9);"> 函数 vs. 方法</font>
<font style="color:rgb(0, 0, 0);">Python 使用 </font>`<font style="color:rgb(0, 0, 0);">def</font>`<font style="color:rgb(0, 0, 0);">关键字定义函数，无需指定参数和返回值的类型。</font>

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



### <font style="color:rgba(0, 0, 0, 0.9);">3. </font><font style="color:rgba(0, 0, 0, 0.9);">🧱</font><font style="color:rgba(0, 0, 0, 0.9);"> 代码块与缩进</font>


<font style="color:rgb(0, 0, 0);">Python 使用冒号(</font>`<font style="color:rgb(0, 0, 0);">:</font>`<font style="color:rgb(0, 0, 0);">)和</font>**<font style="color:rgb(0, 0, 0);">缩进</font>**<font style="color:rgb(0, 0, 0);">（通常4个空格）来定义代码块，缩进是语法的一部分。</font>

_<font style="color:rgb(0, 0, 0);">Python 依靠缩进层级区分代码块。</font>_

```python
if age >= 18:
    print("成年")
    print("可以投票了")  # 这行也在if块内
else:
    print("未成年")
print("程序继续")  # 这行已在if-else块之外
```



<font style="color:rgb(0, 0, 0);">Python 和 Java 在代码书写上存在显著差异，这主要源于它们不同的设计哲学。Python 追求 </font>**<font style="color:rgb(0, 0, 0);">简洁明了</font>**<font style="color:rgb(0, 0, 0);"> 和 </font>**<font style="color:rgb(0, 0, 0);">开发效率</font>**<font style="color:rgb(0, 0, 0);">，而 Java 则更强调 </font>**<font style="color:rgb(0, 0, 0);">严谨清晰</font>**<font style="color:rgb(0, 0, 0);"> 和 </font>**<font style="color:rgb(0, 0, 0);">类型安全</font>**

。

<font style="color:rgb(0, 0, 0);">下面是一个快速了解两者主要书写差异的表格：</font>

| <font style="color:rgb(0, 0, 0);">特性</font> | <font style="color:rgb(0, 0, 0);">Python</font> | <font style="color:rgb(0, 0, 0);">Java</font> |
| :--- | :--- | :--- |
| **<font style="color:rgb(0, 0, 0);">代码块</font>** | <font style="color:rgb(0, 0, 0);">缩进（通常4空格）</font> | <font style="color:rgb(0, 0, 0);">大括号</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">{}</font>` |
| **<font style="color:rgb(0, 0, 0);">语句结束</font>** | <font style="color:rgb(0, 0, 0);">通常无需分号</font> | <font style="color:rgb(0, 0, 0);">必须使用分号</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">;</font>` |
| **<font style="color:rgb(0, 0, 0);">变量类型</font>** | <font style="color:rgb(0, 0, 0);">动态类型，无需声明</font> | <font style="color:rgb(0, 0, 0);">静态类型，必须声明</font> |
| **<font style="color:rgb(0, 0, 0);">函数/方法</font>** | `<font style="color:rgb(0, 0, 0);">def</font>`<font style="color:rgb(0, 0, 0);">定义，无需类型声明</font> | <font style="color:rgb(0, 0, 0);">需指定返回类型和参数类型</font> |
| **<font style="color:rgb(0, 0, 0);">主程序入口</font>** | <font style="color:rgb(0, 0, 0);">无特定方法，脚本即执行</font> | `<font style="color:rgb(0, 0, 0);">public static void main</font>` |
| **<font style="color:rgb(0, 0, 0);">注释</font>** | `<font style="color:rgb(0, 0, 0);">#</font>`<font style="color:rgb(0, 0, 0);">单行，</font>`<font style="color:rgb(0, 0, 0);">'''</font>`<font style="color:rgb(0, 0, 0);">或</font>`<font style="color:rgb(0, 0, 0);">"""</font>`<font style="color:rgb(0, 0, 0);">多行</font> | `<font style="color:rgb(0, 0, 0);">//</font>`<font style="color:rgb(0, 0, 0);">单行，</font>`<font style="color:rgb(0, 0, 0);">/* */</font>`<font style="color:rgb(0, 0, 0);">多行</font> |
| **<font style="color:rgb(0, 0, 0);">文档字符串</font>** | `<font style="color:rgb(0, 0, 0);">"""</font>`<font style="color:rgb(0, 0, 0);">文档字符串，运行时可访问</font> | `<font style="color:rgb(0, 0, 0);">/** */</font>`<font style="color:rgb(0, 0, 0);">Javadoc，生成API文档</font> |


<font style="color:rgb(0, 0, 0);">接下来我们看一些具体的代码示例。</font>

### <font style="color:rgba(0, 0, 0, 0.9);">1. </font><font style="color:rgba(0, 0, 0, 0.9);">🔍</font><font style="color:rgba(0, 0, 0, 0.9);"> 变量定义</font>
<font style="color:rgb(0, 0, 0);">Python 是动态类型语言，变量无需声明类型，类型在运行时确定</font>

。

```plain
name = "Alice"  # 字符串
age = 30        # 整数
score = 95.5    # 浮点数
is_pass = True  # 布尔值
```

_<font style="color:rgb(0, 0, 0);">Python 中变量直接赋值，类型自动推断。</font>_

<font style="color:rgb(0, 0, 0);">Java 是静态类型语言，变量必须显式声明类型</font>

。

```plain
String name = "Alice"; // 必须声明为String
int age = 30;          // 必须声明为int
double score = 95.5;   // 必须声明为double
boolean isPass = true; // 必须声明为boolean
```

_<font style="color:rgb(0, 0, 0);">Java 中每个变量都必须先声明其类型。</font>_

### <font style="color:rgba(0, 0, 0, 0.9);">2. </font><font style="color:rgba(0, 0, 0, 0.9);">🔧</font><font style="color:rgba(0, 0, 0, 0.9);"> 函数 vs. 方法</font>
<font style="color:rgb(0, 0, 0);">Python 使用</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">def</font>`<font style="color:rgb(0, 0, 0);">关键字定义函数，无需指定参数和返回值的类型</font>

。

```plain
def add(a, b):    # 无需类型声明
    return a + b

result = add(5, 3)  # 可以传递整数
result2 = add("Hello, ", "World!")  # 也可以传递字符串，连接起来
```

_<font style="color:rgb(0, 0, 0);">Python 函数定义灵活，但调用时需注意参数类型。</font>_

<font style="color:rgb(0, 0, 0);">Java 中方法（函数）必须在类中定义，需明确指定参数和返回值的类型</font>

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

_<font style="color:rgb(0, 0, 0);">Java 方法定义严格，类型安全在编译期检查。</font>_

### <font style="color:rgba(0, 0, 0, 0.9);">3. </font><font style="color:rgba(0, 0, 0, 0.9);">🧱</font><font style="color:rgba(0, 0, 0, 0.9);"> 代码块与缩进</font>
<font style="color:rgb(0, 0, 0);">Python 使用冒号(</font>`<font style="color:rgb(0, 0, 0);">:</font>`<font style="color:rgb(0, 0, 0);">)和</font>**<font style="color:rgb(0, 0, 0);">缩进</font>**<font style="color:rgb(0, 0, 0);">（通常4个空格）来定义代码块，缩进是语法的一部分</font>

。

```plain
if age >= 18:
    print("成年")
    print("可以投票了")  # 这行也在if块内
else:
    print("未成年")
print("程序继续")  # 这行已在if-else块之外
```

_<font style="color:rgb(0, 0, 0);">Python 依靠缩进层级区分代码块。</font>_

_<font style="color:rgb(0, 0, 0);"></font>_

_<font style="color:rgb(0, 0, 0);"></font>_

<font style="color:rgb(0, 0, 0);">Java 使用</font>**<font style="color:rgb(0, 0, 0);">大括号</font>****<font style="color:rgb(0, 0, 0);"> </font>**`**<font style="color:rgb(0, 0, 0);">{}</font>**`<font style="color:rgb(0, 0, 0);"> 来定义代码块，缩进主要用于提升可读性</font>

_<font style="color:rgb(0, 0, 0);">Java 用花括号明确代码块边界，缩进是风格问题。</font>_  
 

```java
if (age >= 18) {
    System.out.println("成年");
    System.out.println("可以投票了");
} else {
    System.out.println("未成年");
}
System.out.println("程序继续");
```







### <font style="color:rgba(0, 0, 0, 0.9);">4. </font><font style="color:rgba(0, 0, 0, 0.9);">🐘</font><font style="color:rgba(0, 0, 0, 0.9);"> 面向对象</font>
<font style="color:rgb(0, 0, 0);">Python 定义类使用 </font>`<font style="color:rgb(0, 0, 0);">class</font>`<font style="color:rgb(0, 0, 0);">，构造方法名为 </font>`<font style="color:rgb(0, 0, 0);">__init__</font>`<font style="color:rgb(0, 0, 0);">，实例方法第一个参数通常是 </font>`<font style="color:rgb(0, 0, 0);">self</font>`<font style="color:rgb(0, 0, 0);">（代表实例本身)</font>。

_<font style="color:rgb(0, 0, 0);">Python 的面向对象语法更简洁。</font>_

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



<font style="color:rgb(0, 0, 0);">Java 定义类使用 </font>`<font style="color:rgb(0, 0, 0);">class</font>`<font style="color:rgb(0, 0, 0);">，构造方法名与类名相同，使用 </font>`<font style="color:rgb(0, 0, 0);">this</font>`<font style="color:rgb(0, 0, 0);">关键字引用当前实例。</font>

_<font style="color:rgb(0, 0, 0);">Java 的面向对象语法更正式严谨，封装性更强</font>_

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



### <font style="color:rgba(0, 0, 0, 0.9);">5. </font><font style="color:rgba(0, 0, 0, 0.9);">💬</font><font style="color:rgba(0, 0, 0, 0.9);"> 注释与文档</font>
<font style="color:rgb(0, 0, 0);">Python 使用</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">#</font>`<font style="color:rgb(0, 0, 0);">进行单行注释，使用三引号</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">'''</font>`<font style="color:rgb(0, 0, 0);">或</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">"""</font>`<font style="color:rgb(0, 0, 0);">进行多行注释或作为文档字符串 (Docstring)</font>

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

_<font style="color:rgb(0, 0, 0);">Python 的文档字符串是语言特性，可用于自动生成文档或在运行时查看。</font>_

<font style="color:rgb(0, 0, 0);">Java 使用</font><font style="color:rgb(0, 0, 0);"> </font>`<font style="color:rgb(0, 0, 0);">//</font>`<font style="color:rgb(0, 0, 0);">进行单行注释，</font>`<font style="color:rgb(0, 0, 0);">/* */</font>`<font style="color:rgb(0, 0, 0);">进行多行注释，</font>`<font style="color:rgb(0, 0, 0);">/** */</font>`<font style="color:rgb(0, 0, 0);">用于生成 Javadoc 文档</font>

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

_<font style="color:rgb(0, 0, 0);">Java 的 Javadoc 注释通过工具生成离线API文档。</font>_

### <font style="color:rgba(0, 0, 0, 0.9);">6. </font><font style="color:rgba(0, 0, 0, 0.9);">🎨</font><font style="color:rgba(0, 0, 0, 0.9);"> 特有语法</font>
<font style="color:rgb(0, 0, 0);">Python 提供了一些</font>**<font style="color:rgb(0, 0, 0);">语法糖</font>**<font style="color:rgb(0, 0, 0);">让代码更简洁。</font>

**<font style="color:rgb(0, 0, 0);">列表推导式</font>**<font style="color:rgb(0, 0, 0);">：快速生成列表</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

```python
squares = [x**2 for x in range(10)] # [0, 1, 4, 9, ..., 81]
```

**<font style="color:rgb(0, 0, 0);">切片</font>**<font style="color:rgb(0, 0, 0);">：优雅处理序列的子集</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

```python
my_list = [0, 1, 2, 3, 4, 5]
sub_list = my_list[1:4]  # [1, 2, 3]
```

**<font style="color:rgb(0, 0, 0);">f-string</font>**<font style="color:rgb(0, 0, 0);">：灵活的字符串格式化（Python 3.6+）</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

```python
name = "Alice"
age = 30
greeting = f"Hello, {name}. You are {age} years old."
```

<font style="color:rgb(0, 0, 0);">Java 的语法特性更注重</font>**<font style="color:rgb(0, 0, 0);">类型安全</font>**<font style="color:rgb(0, 0, 0);">和</font>**<font style="color:rgb(0, 0, 0);">结构严谨</font>**<font style="color:rgb(0, 0, 0);">。</font>

**<font style="color:rgb(0, 0, 0);">泛型</font>**<font style="color:rgb(0, 0, 0);">：提供编译时类型检查</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

```java
List<String> list = new ArrayList<>(); // 只能存放String
list.add("Hello");
// list.add(42); // 编译错误
```

**<font style="color:rgb(0, 0, 0);">注解</font>**<font style="color:rgb(0, 0, 0);">：为代码添加元数据</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

```java
@Override // 注解，表示方法重写
public void introduce() { ... }
```

### <font style="color:rgba(0, 0, 0, 0.9);">💎</font><font style="color:rgba(0, 0, 0, 0.9);"> 总结</font>
<font style="color:rgb(0, 0, 0);">Python 和 Java 的书写风格差异巨大，这体现了它们不同的设计哲学：</font>

**<font style="color:rgb(0, 0, 0);">Python</font>**<font style="color:rgb(0, 0, 0);"> 像</font>**<font style="color:rgb(0, 0, 0);">“写笔记”</font>**<font style="color:rgb(0, 0, 0);">，</font>**<font style="color:rgb(0, 0, 0);">简洁灵活</font>**<font style="color:rgb(0, 0, 0);">，追求开发效率和表达力，适合快速原型、脚本、数据科学和AI</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

**<font style="color:rgb(0, 0, 0);">Java</font>**<font style="color:rgb(0, 0, 0);"> 像</font>**<font style="color:rgb(0, 0, 0);">“写正式报告”</font>**<font style="color:rgb(0, 0, 0);">，</font>**<font style="color:rgb(0, 0, 0);">严谨清晰</font>**<font style="color:rgb(0, 0, 0);">，强调结构、类型安全和可维护性，适合大型企业应用、复杂后端系统和Android开发</font>

+ <font style="color:rgb(0, 0, 0);">。</font>

