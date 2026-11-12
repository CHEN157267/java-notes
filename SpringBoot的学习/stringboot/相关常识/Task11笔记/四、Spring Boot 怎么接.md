---
title: 四、Spring Boot 怎么接
url: https://www.yuque.com/ehsuh/pggizs/iiac1692rg36l33z
doc_id: 291171637
exported_at: 2026-11-12T23:14:53
---

### 4.1 依赖：不写版本
```plain
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

版本由 `spring-boot-starter-parent` 管（实测解析到 3.5.16）。**parent 里没有的依赖才要自己写版本** —— 不写又没管的，Maven 直接构建失败（不是警告）。

命名规律：官方 starter 形如 `spring-boot-starter-<能力>`，`data-*` 是数据访问家族。

### 4.2 配置：Boot 3 换前缀了
```plain
spring.data.redis.host=localhost
spring.data.redis.port=6379
```

| 版本 | 写法 |
| --- | --- |
| Spring Boot 2.x | `spring.redis.host` |
| Spring Boot 3.x | `spring.data.redis.host` |


**写错前缀不报错，只是静默失效** —— 你以为配了，实际用的是默认值。

### 4.3 ★ 两个 "data"，不是一回事
| 长得像 | 在哪 | 管什么 |
| --- | --- | --- |
| `spring-boot-starter-**data**-redis` | pom.xml | 装哪些 jar |
| `spring.**data**.redis.host` | application.properties | 配置项叫什么名 |


Boot 3 干的事只是**搬配置前缀**，它没改依赖。这两个 `data` 只是名字撞了。

### 4.4 用哪个模板
| | `RedisTemplate` | `StringRedisTemplate` |
| --- | --- | --- |
| key/value 类型 | 任意（需配序列化器） | **只能 String** |
| 默认序列化 | JDK 二进制（`keys *` 看到 `\xac\xed...` 乱码） | String |
| 适合 | 存对象（配 Jackson 序列化器） | **存 JSON 文本**（本项目） |


选了 `StringRedisTemplate`，就得自己把对象转 JSON —— 换来的是 `keys *` 里能直接看到 `user:list` 这种可读的 key。

