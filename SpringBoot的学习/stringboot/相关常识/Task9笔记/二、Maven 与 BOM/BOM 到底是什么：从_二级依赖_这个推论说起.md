---
title: BOM 到底是什么：从"二级依赖"这个推论说起
url: https://www.yuque.com/ehsuh/pggizs/epg14o1kxh02ha5i
doc_id: 289233939
exported_at: 2026-10-22T23:47:26
---

## 一、原话（保留）
"dependencyManagement 这里的 dependency 不是直接写 version，而是跟常规依赖一样的写法，只是把 version 放到 properties 里，多了 type 和 scope。 我在想，这应该是**类似于二级依赖**吧 —— type 和 scope 告诉 Spring：这个不是依赖，而依赖应该是被整理到 `spring-ai-bom` 里面的；这个 version 应该是 **bom 的 version**。 因为我们的 pom 除了 bom 之外，只多写了一个 DeepSeek 的依赖，所以才有这个猜想。"

---

## 二、这个推论对在哪 ✅
| 你的判断 | 对不对 | 说明 |
| --- | --- | --- |
| `type` + `scope` 是在说"我不是依赖" | ✅ 对 | `type=pom` + `scope=import` 正是"导入清单"的固定写法 |
| 那个 version 是 **BOM 的** version | ✅ 对 | 写的是 BOM 文件自己的版本（1.1.8） |
| 我们要的依赖"在 BOM 里面" | ✅ 基本对 | BOM 里确实是一堆依赖的版本规定 |
| "二级依赖"这个直觉 | ✅ **很准** | 一级是"规则"，二级才是"引入" |


---

## 三、补精确的三处
### 3.1 BOM 是什么文件
**它就是一份普通的 pom 文件**，里面**只有 **`**<dependencyManagement>**`**，没有 **`**<dependencies>**`。

```plain

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.ai</groupId>
            <artifactId>spring-ai-starter-model-deepseek</artifactId>
            <version>1.1.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.ai</groupId>
            <artifactId>spring-ai-model</artifactId>
            <version>1.1.8</version>
        </dependency>
        
    </dependencies>
</dependencyManagement>
```

**注意：它是"规定"，不是"东西"** —— BOM 本身不会让任何 jar 被下载。

### 3.2 `import` 干了什么：**合并，不是嵌套**
```plain
BOM 里的十几条规则
        ↓  scope=import（等价于"复制粘贴"）
你的 dependencyManagement
        ↓  现在你的 pom 也"知道"这些版本了
你在 dependencies 里写 starter（不写 version）
        ↓  Maven 去你的规则表里查
查到 1.1.8  →  下载
```

**所以不是"依赖存在 BOM 里、运行时去 BOM 拿"** —— 是**编译期把规则抄过来**，之后 BOM 就不参与了。

### 3.3 "二级"的准确说法
| 层 | 位置 | 干什么 |
| --- | --- | --- |
| **规则层** | `dependencyManagement`（含 `import` 进来的 BOM） | 只规定版本，**不引入任何 jar** |
| **引入层** | `dependencies` | 真正让 Maven 下载 jar |


**两者缺一不可**：

+ 只有规则、没有引入 → **什么都不会下载**
+ 只有引入、没有规则 → 每条都得自己写 version，**还可能互相不兼容**

---

## 四、为什么必须要有 BOM（不用行不行）
**行，但你要自己写十几个 version，而且必须保证它们互相兼容。**

BOM 的价值不只是"省事"，是：**这一套版本被官方验证过能一起工作**。

**我们实测的证据**：加完 BOM，`dependency:build-classpath` 出来的 **15 个 spring-ai jar 全部是 1.1.8**，一个不差。

（对比 Task7 的教训：Knife4j 4.5.0 里传递了 springdoc 2.3.0，跟 Boot 3.5 不兼容 → 编译过、运行 `NoSuchMethodError`。**版本不兼容不会在编译期报错**，这正是 BOM 存在的理由。）

---

## 五、三个容易混的点
### ① BOM 的 version ≠ 你要引入的依赖的 version
```plain
<dependency>
    <artifactId>spring-ai-bom</artifactId>
    <version>${spring-ai.version}</version>   ← 这是 BOM 文件自己的版本
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

你的 starter **不写 version**，因为规则表里有。

### ② `dependencyManagement` 不一定要用 BOM
```plain
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.例子</groupId>
            <artifactId>x</artifactId>
            <version>1.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

这样也能"统一版本"，只是要**一条条自己写**。  
**BOM 就是"别人替你写好的那一堆"。**

### ③ `scope=import` 有硬性限制
+ **只能配 **`**type=pom**`
+ **只能出现在 **`**<dependencyManagement>**`** 里**
+ 写在 `<dependencies>` 里会报错

---

## 六、一句话总结
**BOM = 一份"只有版本规定、没有依赖引入"的 pom。**`**import**`** = 把它的规定抄进你的规则表。****真正下载 jar 的，永远是 **`**<dependencies>**`**。**

所以你的"二级依赖"其实可以说得更准一点： **它不是"二级依赖"，是"一级规则 + 二级引入"两层结构** —— 你的直觉抓到了"两层"，只是把"规则"也叫成了"依赖"。



