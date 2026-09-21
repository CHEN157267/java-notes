---
title: Wrapper家族
url: https://www.yuque.com/ehsuh/pggizs/wnacxexpknlgob9z
doc_id: 286007546
exported_at: 2026-09-21T23:02:34
---

`rapper<T>` 是**抽象类，不能 new**（写 `new Wrapper<User>()` 必报错——这是设计如此，不是写错）。

| 类 | 用途 | 列名写法 |
| --- | --- | --- |
| `QueryWrapper` | 查 / 删 | 字符串 `"create_time"` |
| `LambdaQueryWrapper` | 查 / 删 | 方法引用 `User::getCreateTime`（**写错编译期就报红**） |
| `UpdateWrapper` | 更新 | 字符串，**有 **`**.set()**`** 可显式赋值** |
| `LambdaUpdateWrapper` | 更新 | 方法引用 |




**问题一：你是查还是改？**

+ 查、删、统计 → `QueryWrapper`
+ **改** → `UpdateWrapper`

这就是我之前埋的那个雷的答案：`updateById` 跳过 null，改不了字段为 null 的值。`**UpdateWrapper**`** 就是解决它的**——它有个 `.set()`，你想把字段改成什么（包括 null）都能显式指定，不走"跳过 null"那套。

