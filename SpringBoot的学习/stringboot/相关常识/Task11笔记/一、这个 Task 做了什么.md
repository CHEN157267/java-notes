---
title: 一、这个 Task 做了什么
url: https://www.yuque.com/ehsuh/pggizs/vyxrfdogvg0g16gl
doc_id: 291170111
exported_at: 2026-11-12T23:14:51
---

给现有的 `/user/list` 加一层 Redis 缓存：

| 动作 | 结果 |
| --- | --- |
| 装 Redis 7.4.2（老师发的 Windows 原生包） | `redis-cli ping` → `PONG` |
| 加 `spring-boot-starter-data-redis` | 版本由 parent 管理（3.5.16 + lettuce 6.6.0） |
| `getUser()` 先查缓存，未命中回源 | key = `user:list`，TTL 30 秒 |
| `add/update/delete` 成功后清缓存 | 数据一变，缓存立即作废 |
| 验证 | 第 1 次有 SQL + "未命中"日志；第 2/3 次只有"命中"日志，零 SQL |


