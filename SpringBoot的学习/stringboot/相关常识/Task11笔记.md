---
title: Task11笔记
url: https://www.yuque.com/ehsuh/pggizs/wt6vbekorn1e43u3
doc_id: 291111059
exported_at: 2026-11-12T23:14:49
---

本页 = 索引 + 尾部章节



## 一张图记住整条链路
```plain
GET /user/list
   ↓
getUser()
   ↓
String json = redis.get("user:list")   ──── 命中 ──→ readValue(json) → List<User> ──┐
   ↓ 未命中                                                                          │
userMapper.selectList(null)  ← MyBatis ← JDBC ← MySQL                                │
   ↓                                                                                 │
json = writeValueAsString(list)                                                      │
redis.set("user:list", json, 30s)                                                    │
   ↓                                                                                 │
return list ──────────────────────────────────────────────────────────────────────────┤
                                                                                     ↓
                                                              Result.success(list)
                                                                     ↓
                                                     Spring MVC + Jackson → JSON 响应体
```







## 九、验收记录（2026-11-07 实测）
### 9.1 缓存命中
| 轮次 | 耗时 | 请求后 TTL | 说明 |
| --- | --- | --- | --- |
| 第 1 次 | 486 ms | 30 | 未命中 → 回源 → 写入 |
| 等 4 秒 | — | 22 | 正常倒计时 |
| 第 2 次 | 6.7 ms | **22（没重置）** | 命中 |
| 第 3 次 | 2.5 ms | 22 | 命中 |


**TTL 不重置**才是"没回源"的铁证 —— 如果每次都查库，`set` 会把 TTL 拉回 30。

### 9.2 日志证据（控制台原文摘录）
```plain
==>  Preparing: SELECT id,username,password,create_time FROM user
<==      Total: 10
缓存未命中：回源查库并写入缓存                    ← 第 1 次
缓存命中：从 Redis 读取用户列表                    ← 第 2 次，无 SQL
缓存命中：从 Redis 读取用户列表                    ← 第 3 次，无 SQL
```

### 9.3 失效验证（用临时用户，净变化为零）
| 步骤 | 观察 |
| --- | --- |
| ① `GET /user/list` | 缓存 TTL=30 |
| ② `POST /user/add`（cachelogin） | 返回 `{"id":19,...}` |
| ③ 查 Redis | **keys 空** → 已失效 |
| ④ 再 `GET /user/list` | 未命中，列表里**能看到新人** |
| ⑤ `DELETE /user/delete/19` | 成功，缓存再次失效 |
| ⑥ 再查 | 新人已消失，数据一致 |


顺带验证：`add` 的响应里**没有 password** —— `@JsonProperty(WRITE_ONLY)` 生效。

---

## 十、速记表（贴在显示器上）
| 问题 | 答案 |
| --- | --- |
| Redis 是什么 | 独立进程里的 `Map<String, byte[]>` |
| 为什么不用 Map | 多机共享 / 不占 JVM 堆 / 有 TTL 与淘汰 / 可持久化 |
| 启动带什么 | `redis-server.exe redis.conf`（双击 = 没参数 = 默认配置） |
| Boot 3 配置前缀 | `spring.data.redis.*` |
| 序列化出什么 | JSON → `String`；JDK → `byte[]` |
| 反序列化缺什么 | 泛型 → `TypeReference`；构造器/setter 缺了会炸 |
| 什么时候删缓存 | **数据一变就删**，不是等它过期 |
| 三坑 | 穿透（不存在）、击穿（单个热点过期）、雪崩（一批同时过期） |
| 抢锁命令 | `SET k v NX EX 10` |


---

## 十一、遗留与后续
1. `**@TableField(select=false)**`** 的后遗症**：以后做登录，查不到密码 —— 需要单独写带列的查询。
2. **生产环境日志**：MyBatis 会把结果集每行打出来（含 password），生产要调 `logging.level...mapper=info`。
3. **库里还有明文密码的老数据**（Task5 之前插入的 1~3 条），以后清洗。
4. **降级缺两道保险**：Redis 超时要设短（否则每请求都卡住），并加熔断（连续失败后一段时间直接跳过）。
5. **单机 Redis 无高可用**：生产要哨兵/集群。
6. `**user:list**`** 是全表缓存**：数据量大时该分页缓存或按 id 缓存。

