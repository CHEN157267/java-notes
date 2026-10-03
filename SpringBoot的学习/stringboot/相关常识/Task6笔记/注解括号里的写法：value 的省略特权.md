---
title: 注解括号里的写法：value 的省略特权
url: https://www.yuque.com/ehsuh/pggizs/gc1exayiuroo1ul1
doc_id: 246188195
exported_at: 2026-10-03T22:20:32
---

### 括号里写的是什么
```plain

```

三个部分：**属性名 → **`**=**`** → 值**。

### 为什么这里必须写 `access =`，而别的地方能省？
**Java 规则**：**注解里那个叫 **`**value**`** 的属性，赋值时可以省掉 **`**value = **`**。**

```plain
@JsonProperty(access = WRITE_ONLY)
              └属性名┘ └─值─┘
```

**只在属性名恰好是 **`**value**`** 时才能省，跟属性总数无关。**

编译器实测（本机 javac 跑的）：

| 测试 | 结果 |
| --- | --- |
| `@JsonProperty("pwd")` 省略属性名 | ✅ `exit=0` |
| `@NotBlank("...")` 省略属性名 | ❌ **编译失败：找不到符号 方法 value()** |


`**JsonProperty**`** 有 7 个属性**（`value / namespace / required / isRequired / index / defaultValue / access`），`value` 照样能省。 `**NotBlank**`** 只有 3 个**（`message / groups / payload`），**恰恰没有 **`**value**` → **不能省**。

**注解属性不是"方法形参"**：

+ 它长得像方法（`String value();`），其实是**属性的声明**，编译器借方法形式存属性
+ **类型是注解定义时就定死的**（`value` 是 String，`access` 是 `Access`），不是你传的时候挑的

