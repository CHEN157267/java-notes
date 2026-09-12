---
title: JAVA中的注意事项
url: https://www.yuque.com/ehsuh/oguki0/lw7blwht8qc4quw1
doc_id: 269971242
exported_at: 2026-09-12T09:31:41
---

arr.forr:数组倒着遍历

为了避免if的多层嵌套导致史山代码，可以在循环里面通过if来判断不符合要求的值，再直接continue，而后续的代码再写在这个if之后

在JAVAbean中，boolean类型的变量不是get…而是叫is…

String Builder 的append方法的返回值是this，所以可以连续使用append添加数据

sb.append("1").append("2")

