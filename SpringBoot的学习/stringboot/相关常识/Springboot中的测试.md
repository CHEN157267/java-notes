---
title: Springboot中的测试
url: https://www.yuque.com/ehsuh/pggizs/igs3i2t8bo29tb14
doc_id: 286342052
exported_at: 2026-09-27T10:04:54
---

+ `@SpringBootTest` 虽然叫"测试"，但它真的会**把整个 Spring 跑起来** ✅
+ 手写测试代码放在 `test` 文件夹下、用 `@Test` 运行 ✅

| **方法头上写了什么** | **跑起来会怎样** | **这种叫** |
| --- | --- | --- |
| **只有**** **`**@Test**` | 什么都不启动，你自己 `new`<br/> 对象 | 单元测试 |
| `**@Test**`<br/>** ****+**** **`**@SpringBootTest**` | 先启动完整 Spring 容器，再把依赖注进来 | 集成测试 |


`**@Test**`** 是入场券，**`**@SpringBootTest**`** 是可选加料。**

**两种测试都必须有 **`**@Test**`（没有它 JUnit 根本不认识这个方法），区别只在**要不要再加 **`**@SpringBootTest**`。

"手写测试"的定义特征**不是"手写"**（集成测试的代码也是手写的），而是"**不启动 Spring**"。



test 文件夹 + @Test、@Test 是必要的、@SpringBootTest 会真的启动 Spring、没启动 Spring 就没有 bean 所以要手动 new。

如果是 private 的构造器的话，你敲下 `new UserServiceImpl(fakeMapper)` 那一刻，IDEA 立刻标红，`mvn compile` 直接失败。**你根本没有"点运行"的机会**，因为代码压根编译不出来。

