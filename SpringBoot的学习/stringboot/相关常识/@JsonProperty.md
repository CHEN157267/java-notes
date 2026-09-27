---
title: @JsonProperty
url: https://www.yuque.com/ehsuh/pggizs/ksuw04p04pdc705b
doc_id: 257126371
exported_at: 2026-09-27T10:04:49
---

@JsonProperty括号里写的是什么

三个部分：access（属性名） → = → 值。



为什么这里必须写 access =，而 @NotBlank 可以省？

```plain
@JsonProperty(access = WRITE_ONLY)      // 必须写属性名
@NotBlank(message = "用户名不能为空")     // 也可以写成 @NotBlank("用户名不能为空")

```

Java 有条规则：**注解里那个叫 **`**value**`** 的属性，可以直接写值省略属性名。**

+ `@NotBlank` 的 `message` 就是 `value` 的别名 → **能省**
+ `@JsonProperty` 的属性有 `value`、`access`、`required`… 而我们要设的是 `**access**`** ****不是**** **`**value**` → **必须写全**

所以不是"有的注解要写有的不用"，是**你要设的那个属性恰好叫不叫**** **`**value**`。

（顺带：你想拿 `@JsonIgnore` 图省事的话要注意——它是**双向全禁**，前端传来的 password 会被直接丢掉，`user.getPassword()` 变 null，`encode(null)` 直接炸。你 WIRTE_ONLY 选对了。）

