---
title: updatebyid的详解
url: https://www.yuque.com/ehsuh/pggizs/ca7omrc7s2np9kx6
doc_id: 286054727
exported_at: 2026-09-24T19:26:33
---

updateById 只更新非 null 字段

| 出口 | 含义 |
| :--- | :--- |
| 返回 1 | 真的改了 |
| 返回 0 | ① id 不存在 ② 值没变 |
| **抛异常** | 约束冲突 / 连接断开 |


