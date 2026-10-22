---
title: 二、Maven 与 BOM
url: https://www.yuque.com/ehsuh/pggizs/uifis9m4a2mp7fk3
doc_id: 289216280
exported_at: 2026-10-22T23:47:26
---

### 1 BOM 是什么
**BOM = Bill of Materials（物料清单）**：一份"**这套东西用哪个版本**"的清单。

Spring AI 拆成十几个模块（`starter-model-deepseek` / `model` / `client-chat` / `commons` / `retry` …），**版本必须一致**，否则会出现"编译过、运行时 `NoSuchMethodError`"（Task7 就是这么炸的）。

### 2 怎么用
```plain
<properties>
    <spring-ai.version>1.1.8</spring-ai.version>
</properties>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.ai</groupId>
            <artifactId>spring-ai-bom</artifactId>
            <version>${spring-ai.version}</version>
            <type>pom</type>        
            <scope>import</scope>   
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
    <dependency>
        <groupId>org.springframework.ai</groupId>
        <artifactId>spring-ai-starter-model-deepseek</artifactId>
        
    </dependency>
</dependencies>
```

`**dependencyManagement**`** 只"定规矩"，不"下载东西"**

+ 它不引入任何 jar，只规定"这些模块用哪个版本"
+ 真正引入还是靠 `<dependencies>`

`**type=pom**`** + **`**scope=import**`** 是固定组合**

+ 意思是"**导入清单**"，不是"引入依赖"
+ 只有 `dependencyManagement` 里能这么用

**pom 的 **`**<properties>**`** 是"构建期变量"**

+ 标签名 = 变量名，标签体 = 值（`<spring-ai.version>1.1.8</spring-ai.version>` 等价于 `spring-ai.version = "1.1.8"`）
+ 引用：`${spring-ai.version}`（**美元在前**，不是 `{$...}`）
+ **它在编译/打包时就被替换掉了**，打完包就"用完即弃"

