---
title: Error 和 Exception 是「平级兄弟」
url: https://www.yuque.com/ehsuh/pggizs/iapgr1cotgdgbgvw
doc_id: 287165238
exported_at: 2026-10-06T10:13:25
---

```plain
Throwable
 ├─ Error          ← 程序处理不了的错误
 │   └─ NoSuchMethodError（版本坑那个）
 └─ Exception      ← 程序能处理的异常
     └─ NoResourceFoundException（favicon 那个）
```

