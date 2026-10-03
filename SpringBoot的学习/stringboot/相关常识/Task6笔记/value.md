---
title: value
url: https://www.yuque.com/ehsuh/pggizs/vyxvnqyt1dfxtcaa
doc_id: 243627078
exported_at: 2026-10-03T22:20:29
---

**精确规则（只此一条）**：

**注解类型（**`**@interface**`**）里，如果定义了一个名叫 **`**value**`** 的成员，给它赋值时可以省掉 **`**value = **`**。**

**跟属性总数无关**：

| **注解** | **属性** | **能省 **`**value = **`** 吗** |
| --- | --- | --- |
| `**JsonProperty**` | **7 个****（**`**value / namespace / required / isRequired / index / defaultValue / access**`**）** | ✅** ****能****（因为有 **`**value**`**）** |
| `**NotBlank**` | **3 个****（**`**message / groups / payload**`**），****没有 **`**value**` | ❌** ****不能** |


**所以密码那行必须写全：**`**@NotBlank(message = "密码不能为空")**`**。**

**其实早就在用这条规则了****：**

```plain
@RequestMapping("/user/list")             // 就是 value 的省略
@RequestMapping(value = "/user/list")     // 等价
```

**不是 **`**JsonProperty**`** 的特权，是 **`**value**`** 这个名字的特权。**

### ⚠️ 两个辅助记忆点
**① 我（小知）在这题上答错过一次** —— 曾说过"`@NotBlank` 的 message 就是 `value` 的别名，也能省"。**是错的**，被编译器"找不到符号 方法 value()"打脸。 **教训：凭印象回答 vs 用编译器验证 —— 这就是差距。**

**② 我追问过"那我自己写的类，字段名叫 **`**value**`**，能省略吗？" → 不能，而且这里根本没东西可省。**

| | 普通类的字段 | 注解（`@interface`）里定义的成员 |
| --- | --- | --- |
| 例子 | `class User { String value; }` | `@interface JsonProperty { String value(); }` |
| 能"省略"吗 | ❌ **无此概念** | ✅ 赋值时可写 `@JsonProperty("x")` 省掉 `value = ` |


**能省的是"给注解赋值时那个 **`**value = **`**"，不是"类里的属性"。** 普通类字段叫 `value`，**不受这条规则影响，也没有任何特权。**

**③ 注解属性 ≠ 方法形参**

它长得像方法（`String value();`），其实是**属性的声明** —— 编译器借方法形式存属性。

+ **类型是注解定义时就定死的**（`value` 是 String，`access` 是 `Access`），不是你传的时候挑的
+ 你写 `@JsonProperty("pwd")` 里的 `"pwd"` 必须是字符串，就因为 `value` 的类型是 String

