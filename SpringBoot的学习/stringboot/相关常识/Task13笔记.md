---
title: Task13笔记
url: https://www.yuque.com/ehsuh/pggizs/eu4rlpget9vihgaq
doc_id: 292985331
exported_at: 2026-11-25T18:28:14
---

## 一  登录链路
二  为什么不能 WHERE password = ?（三层原因）

三  matches 三步 + 哈希串结构 + 47ms 实测

四  两种失败同一句话（用户名枚举）

五  @TableField 两面性 + 动机 ≠ 现状

六  唯一索引（主键对比 / 加索引顺序 / 两道防线）

七  接口设计（POST vs GET/PUT / 幂等 / DTO）

八  日志安全

九  数据库变更（四条 SQL，可复现）

十  遗留



## ①这个 Task 做了什么（速览）
Task5 存了密码哈希，但**从来没校验过**。这个 Task 补上登录：

| 做了什么 | 关键点 |
| --- | --- |
| `dto/LoginRequest` | 只有 username / password + `@NotBlank` |
| `UserMapper.selectForLogin` | `@Select` 手写 SQL，绕过 `@TableField(select=false)` |
| `UserService.login` | 按 username 查 → `matches` 校验 → 失败抛 401 |
| 统一失败提示 | 「用户名或密码错误」，不区分两种情况 |
| 数据库 | 删重复数据 + `uk_username` 唯一索引 |


**明确不做**：token / JWT / session、注册页、找回密码、验证码、权限体系。

---

## ②数据库变更记录（不在 git 里）
```plain
-- 1. 备份被删的那一行
CREATE TABLE user_dup_bak_20261123 AS SELECT * FROM user WHERE id=4;

-- 2. 删掉重复的 zhangsan（保留 id=1，删 id=4）
DELETE FROM user WHERE id=4;

-- 3. 加唯一索引
ALTER TABLE user ADD UNIQUE INDEX uk_username (username);

-- 4. 验证完删备份表
DROP TABLE user_dup_bak_20261123;
```

**结果**：数据从 10 行 → 9 行；`zhangsan` 只剩 id=1；索引 `uk_username`（`NON_UNIQUE=0`）。

## ③★ 错题清单（91 分）
### 1 Q4：不知道“用户名枚举”这个名字（8/12）
概念本身答对了（“防止不端之人获取信息”），但说不出术语。

**记住这个词**：**User Enumeration**。面试和代码审查里都会出现。

### 2 Q6：把“用户名唯一”说成“不唯一”（8/12）
“我们的项目要求用户名不唯一”

**反了。** 正因为要求唯一，才需要 `uk_username`。

这种“说反”已经是第二次（上次是把 POST / PUT 的幂等说反）。**规律：涉及“方向/肯定否定”的表述，写完要回读一遍。**

### 3 附加题：把 `@TableField` 的功劳归错了
我说“它帮忙的是 SQL 日志”，错；他说“它帮忙的是返回前端不带密码”，也错。

**真正的分工**：

+ 返回前端不带密码 → `@JsonProperty(WRITE_ONLY)`
+ 查库时不取这列 → `@TableField(select=false)`
+ “防日志”那个价值 → **已经随着 11-20 关日志而消失**

### 4 一处纠正：SQL 日志不用调全局 debug
正确做法是**只给 mapper 包设**：

```plain
logging.level.com.example.demo.mapper=debug
```

全局调 debug 会让 Spring、Hikari、Tomcat 的日志一起刷屏。

---

## ④验收记录（6 条）
| # | 验收项 | 实测结果 |
| --- | --- | --- |
| 1 | 正确密码登录成功 | `200` + `{id:8, username:"test001"}`，无 password |
| 2 | 密码错误 → 提示统一 | `401 用户名或密码错误` |
| 3 | 用户不存在 → 同一句 | `401 用户名或密码错误`（一字不差） |
| 4 | zhangsan 撞坑 | `TooManyResultsException: found: 2` → 已由唯一索引解决 |
| 5 | 日志无明文 | 4 个测试密码 **0 次**；`登录失败: username=xxx` 正常 |
| 6 | 解释为何不能 `WHERE password=?` | 盐随机，等值比较永不成立 |


**额外验证**：

```plain
直接 SQL 插重复 → ERROR 1062 Duplicate entry 'zhangsan'
走接口插重复   → 409 Username already exists
数据未污染     → 仍 9 行
```

---

## ⑤、速记表
| 概念 | 一句话 |
| --- | --- |
| **不能比哈希** | 库里加盐，明文等值比较永不成立 |
| **不能 encode 再比** | 每次 encode 新盐，结果必然不同 |
| `**matches**`** 三步** | 切盐 → 用盐重算 → 比对 |
| **哈希串结构** | 版本 + 成本 + 盐(22) + 哈希(31) |
| **47ms 的意义** | 你付 1 次，攻击者要付 100 万次 |
| **盐防什么** | 彩虹表（不防单用户暴力破解） |
| **用户名枚举** | 错误提示的差异会泄露“谁存在” |
| **失败提示** | 响应模糊、日志详细 |
| **主键 vs 唯一索引** | 主键管行（允许同名），唯一索引管字段 |
| **两道防线** | 应用层给友好提示，数据库层兜并发 |
| **加索引顺序** | 先清重复，再加索引 |
| **登录用 POST** | 不是 GET（密码进 URL）、不是 PUT（不幂等） |
| **登录不校验格式** | 注册立规矩，登录只认人 |
| **日志** | 记 username，不记 password；一行不记也不行 |


---

## ⑥、遗留
| 项 | 说明 |
| --- | --- |
| `DuplicateKeyException` handler | 并发被唯一索引拒 → 现在走 500，应转 409 |
| 登录限流 | 47ms/次，可被用来打 DoS；Task14 |
| token / session | 只讲了概念，未实现（任务书明确不做） |
| Advisor 统一日志 | Task14 |
| `createTime` 两套序列化 | 给前端是字符串，给模型是数组（Task14） |


