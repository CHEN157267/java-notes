---
title: stream接口中的collect普通方法的形参问题
url: https://www.yuque.com/ehsuh/pggizs/oe9hp9m5omucpvog
doc_id: 283992114
exported_at: 2026-09-12T09:41:12
---

collect 方法的形参类型是 Collector（接口）。

· Collector 不能直接 new，因为它是接口，需要实现类。

· Collectors 是工具类，在这里也叫工厂类，他专门生产collector，提供静态方法（如 toList()、toMap()）返回 Collector 的实现类对象。

· 这些 Collector 实现类对象本身不是 List、Map 或 Set，而是“收集器”，知道怎么把流元素收集成这些集合。

· 把 Collector 对象传给 collect 方法后，collect 方法执行收集逻辑，最终返回你想要的 List、Map 或 Set。

