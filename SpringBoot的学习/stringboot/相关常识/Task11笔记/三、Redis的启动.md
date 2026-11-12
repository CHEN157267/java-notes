---
title: 三、Redis的启动
url: https://www.yuque.com/ehsuh/pggizs/uk3n6iaqhg5l7pkw
doc_id: 291171360
exported_at: 2026-11-12T23:14:53
---

### 3.1 老师给的Redis包
`E:\download\Redis\redis_91947\redis_91947\`，内含 `redis-server.exe` / `redis-cli.exe` / `redis.conf`，版本 **7.4.2**（Windows 64 位，与 Linux 版同源码编译）。

### 3.2 为什么双击不算"启动成功"
Redis 启动时：**先读命令行参数 → 给了配置文件就加载 → 覆盖内置默认值**。

+ 双击 exe：**没有命令行参数** → 用出厂默认（`maxmemory` 不限、`noeviction`、定时存盘）
+ `redis-server.exe redis.conf`：带上参数 → 老师的配置生效（256 MB、`allkeys-lru`、不落盘）

日志里那行 `Warning: no config file specified, using the default config` 就是在提醒这件事。

**验证配置真的生效了**（不是猜）：

```plain
redis-cli config get maxmemory          → 268435456（256 MB）
redis-cli config get maxmemory-policy   → allkeys-lru
redis-cli config get save               → （空）
```

### 3.3 三种启动方式
| 方式 | 做法 | 适合 |
| --- | --- | --- |
| bat | 双击 `启动Redis.bat`（内容 `redis-server.exe redis.conf`） | 日常 |
| 手动 | cmd 里 `redis-server.exe redis.conf` | 想看启动日志 |
| 服务 | 管理员运行 `install_redis.cmd` | 开机自启 |


服务方式本质一样：把 `--service-run "路径\redis.conf"` 写进服务的启动参数里。

