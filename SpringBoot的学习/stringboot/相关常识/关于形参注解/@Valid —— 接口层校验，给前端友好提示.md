---
title: @Valid —— 接口层校验，给前端友好提示
url: https://www.yuque.com/ehsuh/pggizs/fzy2qolaai26ow33
doc_id: 285168324
exported_at: 2026-09-15T10:12:21
---

```java
// 1. 在实体上写规则
public class User {
    @NotBlank(message = "用户名不能为空")
    private String username;
    @NotBlank(message = "密码不能为空")
    private String password;
}

// 2. 在方法上加 @Valid 启用检查
@PostMapping("/add")
public String add(@Valid @RequestBody User user) { ... }

```

+ `@NotBlank(message=...)` 里的 `message` = 规则不通过时要说的"人话"
+ `@Valid` = 贴在参数前，意思是"进方法前，先按这些规则校验一遍"
+ 校验不通过 → Spring 抛异常 → 自动转成 **HTTP 400 + 把 message 放进响应体**
+ 你提的 `getMessage()` 是"异常对象身上的方法，用来取那段 message 文本"——Spring 内部就是调类似机制把 message 取出来返给前端。所以"为了优化用户体验"的直觉完全对，只是把"校验开关(@Valid) + 规则提示(message)"和"取提示的方法(getMessage)"混成一件事了

**两道防线（谁也替代不了谁）：**

+ `@Valid` = 接口层防线，目的是给前端**友好的错误提示**（哪个字段不对）
+ 数据库 NOT NULL = 存储层最后防线，保证"脏数据绝对进不了库"
+ 别人可能绕过你的接口直接操作数据库，所以两道都要有



<!-- 这是一张图片，ocr 内容为：USER @DEMO DB(SQL8 TEST)-表-NAVICAT PREMIUM 收藏夹工具 编辑 查看 帮助 文件 窗口 表 新建查询 查询 模型 自动运行 用户 连接 视图 其它 函数 备份 MYSQL CZH USER@DEMODB(SQL8TEST)-表 对象 USER@DEMO DB(SQL8 TEST) SQL8 TEST 保存 插入字段 删除字段 下移 添加字段 上移 主键 DEMO DB 字段 注释 索引 检查 SQL预览 触发器选项 外键 表 名 类型 小数点 长度 虚拟 不是NULL 键 打开表 ID BIGINT 设计表 50 VARCHAR USERNAME 新建表 100 VARCHAR PASSWORD 删除表 DATETIME CREATE TIME 清空表 截断表 复制表 设置权限 导入向导... 导出向导... 数据生成... 默认: 转储SQL文件 自动递增 打印表 无符号 维护 逆向表到模型... 填充零 创建图表... 管理组 复制 重命名 创建打开表快捷方式... 刷新 字段数:4 -->
![](https://cdn.nlark.com/yuque/0/2026/png/52131016/1789398246560-cfc11fbe-e45d-4553-9c85-a219b0799345.png)设计表这里可以选择是否让该字段的null数据入库

