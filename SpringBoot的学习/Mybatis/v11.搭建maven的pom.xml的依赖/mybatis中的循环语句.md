---
title: mybatis中的循环语句
url: https://www.yuque.com/ehsuh/pggizs/rzyhoe1gl5pghzdq
doc_id: 278775389
exported_at: 2026-09-12T09:41:22
---

```java
<foreach collection="list" item="car" open="(" separator="," close=")">
    #{car.carNum}
</foreach>
```

collection="list"：告诉 MyBatis，你要遍历哪个集合。这里填的是 Map 的 key，或者直接传 List 时默认叫 list。

item="car"：给集合里的每一个元素起个临时名字。就像 for(Car car : carList) 里的 car。

open="("：循环开始前，加个左括号 (

separator=","：每遍历一个元素，后面加个逗号 ,

close=")"：循环结束后，加个右括号 )

标签体里面的内容：就是每次循环要生成的内容。

