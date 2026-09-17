---
title: 增强for循环
url: https://www.yuque.com/ehsuh/oguki0/dgusifwqvfmncx44
doc_id: 219502150
exported_at: 2026-09-12T10:38:44
---

for (元素类型 变量名 : 数组或集合) { // 使用变量访问当前元素 }

```java
ArrayList<Student> students = new ArrayList<>();
students.add(new Student("Alice", 20));
students.add(new Student("Bob", 22));

// 增强 for 循环：直接使用 Student 类型变量
for (Student a : students) {
    System.out.println(a.getName()); // 调用 Student 对象的方法
}
```

### 关键点解析：
1. **泛型类型一致性**  
集合声明为 `ArrayList<Student>`，因此增强 for 循环的元素类型必须是 `Student`，以确保类型匹配。
2. **无需显式类型转换**  
编译器通过泛型已知集合中元素为 `Student`，因此 `a` 直接就是 `Student` 类型，可直接调用其方法（如 `getName()`）。
3. **变量名可自定义**  
`Student a` 中的 `a` 是临时变量名，可任意命名（如 `student`、`s` 等）。

