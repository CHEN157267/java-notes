---
title: static
url: https://www.yuque.com/ehsuh/oguki0/oedoinkupvrpmrao
doc_id: 213946477
exported_at: 2026-09-12T10:38:35
---

<!-- 这是一张图片，ocr 内容为：静态变量是随着类的加载而加载的,优先于对象出现的 STATIC STRING TEACHERNA AME NULL 静态存储位置(静态区) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743820179585-d8cfd980-2e12-43f0-8b76-90588c4af59b.png)





<!-- 这是一张图片，ocr 内容为：STATIC表示静态,是JAVA中的一个修饰符,可以修饰成员方法,成员变量 被STATIC修饰的成员变量,叫做静态变量 被STATIC修饰的成员方法,叫做静态方法 特点: 特点: 多用在测试类和工具类中 被该类所有对象共享 不属于对象,属于类. JAVABEAN类中很少会用 随着类的加载而加载,优先于对象存在 调用方式: 类名调用(推荐) 调用方式: 类名调用(推荐) 对象名调用 对象名调用 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743828880908-fa0bb343-24c2-4760-ac39-ad5805f717d1.png)

static表示静态，是java中的一个修饰符，可以修饰成员方法，成员变量

被static修饰的成员变量，叫做静态变量 被static修饰的成员方法，叫做静态方法



（1）在成员变量中使用static

强调_**<font style="color:#DF2A3F;">共享</font>**_

被该类所有对象共享 不属于对象，**<font style="color:#DF2A3F;">属于类</font>**。

随着类的加载而加载，优先于对象存在

调用方式：

 类名调用（推荐）

对象名调用





<font style="color:rgba(0, 0, 0, 0.85);">(2)在方法中使用static</font>

<font style="color:rgba(0, 0, 0, 0.85);">普通的非静态方法需要先创建类的实例（对象），然后通过对象来调用方法；而被 static 修饰的静态方法属于类本身，可直接通过类名调用，无需创建对象。比如常见的数学工具类</font>`<font style="color:rgba(0, 0, 0, 0.85);">java.util.Math</font>`<font style="color:rgba(0, 0, 0, 0.85);">，其中的</font>`<font style="color:rgba(0, 0, 0, 0.85);">abs</font>`<font style="color:rgba(0, 0, 0, 0.85);">（求绝对值）、</font>`<font style="color:rgba(0, 0, 0, 0.85);">sqrt</font>`<font style="color:rgba(0, 0, 0, 0.85);">（求平方根）等方法都是静态方法，使用时直接</font>`<font style="color:rgba(0, 0, 0, 0.85);">Math.abs(-5)</font>`<font style="color:rgba(0, 0, 0, 0.85);"> 、</font>`<font style="color:rgba(0, 0, 0, 0.85);">Math.sqrt(9)</font>`<font style="color:rgba(0, 0, 0, 0.85);"> 即可，无需创建</font>`<font style="color:rgba(0, 0, 0, 0.85);">Math</font>`<font style="color:rgba(0, 0, 0, 0.85);">类的对象 ，这样能简化代码调用，提高开发效率。</font>





<!-- 这是一张图片，ocr 内容为：STATIC的注意事项 静态方法只能访问静态变量和静态方法 非静态方法可以访问静态变量或者静态方法,也可以访问非静态的成员变量和非静态的成员方法 静态方法中是没有THIS关键字 硬记结论 总结:静态方法中,只能访问静态. 非静态方法可以访问所有. 代码方面理解 静态方法中没有THIS关键字 内存方面理解 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1743898420063-6298f548-0969-4e33-a402-7288848ff4e8.png)

非静态方法是与对象有关的

静态方法是共享的和对象没有太大关系

