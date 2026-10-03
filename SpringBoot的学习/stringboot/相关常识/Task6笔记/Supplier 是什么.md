---
title: Supplier 是什么
url: https://www.yuque.com/ehsuh/pggizs/mgmgg56tu2a322z5
doc_id: 242036901
exported_at: 2026-10-03T22:20:31
---

+ 它是个**函数式接口** = **有且仅有一个抽象方法**（`default`/`static` 不算）
+ `Supplier<T>` 的唯一抽象方法是 `T get()` —— **无参、产出一个值**
+ MyBatis 用它做**延迟求值**：先不拼字符串，等确定真要打日志了才 `get()`，省开销

所以解开报错只要把值包一层：

```plain
log.error("参数错误", e);          // ❌ 直接给值
log.error(() -> "参数错误", e);    // ✅ 给它一个"能产出的东西"
```

`() -> "参数错误"` 读作：**重写那个唯一抽象方法，形参为空，方法体是 **`**return "参数错误"**`。

