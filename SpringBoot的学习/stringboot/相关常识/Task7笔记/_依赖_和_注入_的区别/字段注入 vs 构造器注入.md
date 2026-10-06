---
title: 字段注入 vs 构造器注入
url: https://www.yuque.com/ehsuh/pggizs/ifgt6zftbahxm0f2
doc_id: 287165809
exported_at: 2026-10-06T10:13:31
---

| | `@Autowired` 字段注入 | 构造器注入（你现在的写法） |
| --- | --- | --- |
| 流程 | 先 new 空壳 → 反射塞字段 | 依赖作为构造参数传入 |
| null 窗口 | 有（空壳期调用会 NPE） | 无（出生即完整） |
| final | ❌ 用不了（事后塞值冲突） | ✅ 可用 |
| 缺依赖时 | 启动成功，运行时才 NPE | 启动就炸（早暴露） |
| 单元测试 | 要启动 Spring | 直接 `new Xxx(mock)`，不用 Spring |


**判断标准一句**：这个依赖你能自己 new 出来吗？能 → 自己 new 也行；不能（接口/框架生成）→ 必须注入。

**单构造器时 **`**@Autowired**`** 可省略**（Spring 4.3+），所以你代码里没有 `@Autowired` 是正常且推荐的。

---

