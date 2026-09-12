---
title: 增强for循环
url: https://www.yuque.com/ehsuh/oguki0/dgusifwqvfmncx44
doc_id: 219502150
exported_at: 2026-09-12T10:38:44
---

<font style="color:rgb(28, 31, 35);">for (元素类型 变量名 : 数组或集合) { // 使用变量访问当前元素 }</font>

```java
ArrayList<Student> students = new ArrayList<>();
students.add(new Student("Alice", 20));
students.add(new Student("Bob", 22));

// 增强 for 循环：直接使用 Student 类型变量
for (Student a : students) {
    System.out.println(a.getName()); // 调用 Student 对象的方法
}
```

### <font style="color:rgb(0, 0, 0);">关键点解析：</font>
1. **<font style="color:rgb(0, 0, 0) !important;">泛型类型一致性</font>**<font style="color:rgba(0, 0, 0, 0.85) !important;">  
</font><font style="color:rgba(0, 0, 0, 0.85) !important;">集合声明为</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">ArrayList<Student></font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">，因此增强 for 循环的元素类型必须是</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Student</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">，以确保类型匹配。</font>
2. **<font style="color:rgb(0, 0, 0) !important;">无需显式类型转换</font>**<font style="color:rgba(0, 0, 0, 0.85) !important;">  
</font><font style="color:rgba(0, 0, 0, 0.85) !important;">编译器通过泛型已知集合中元素为</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Student</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">，因此</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">a</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> </font><font style="color:rgba(0, 0, 0, 0.85) !important;">直接就是</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Student</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> </font><font style="color:rgba(0, 0, 0, 0.85) !important;">类型，可直接调用其方法（如</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">getName()</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">）。</font>
3. **<font style="color:rgb(0, 0, 0) !important;">变量名可自定义</font>**<font style="color:rgba(0, 0, 0, 0.85) !important;">  
</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">Student a</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 中的 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">a</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 是临时变量名，可任意命名（如 </font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">student</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">、</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;">s</font>`<font style="color:rgba(0, 0, 0, 0.85) !important;"> 等）。</font>

