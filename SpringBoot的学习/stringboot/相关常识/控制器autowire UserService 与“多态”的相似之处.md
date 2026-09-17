---
title: 控制器autowire UserService 与“多态”的相似之处
url: https://www.yuque.com/ehsuh/pggizs/lpcuogslg7py60gq
doc_id: 285480717
exported_at: 2026-09-17T22:25:41
---

控制器直接 autowire UserService 就像某种多态，**Spring 启动时**会获取符合条件的实现类；如果直接 auto 实现类的话，功能就完全被写死了。

****

`**UserService userService = 某个实现对象**`**，左边接口类型、右边实现对象，这就是多态。注入时 Spring 帮你把"右边"填好了。**

****

+ 如果 `UserService` **只有唯一一个实现**（你现在的情况）→ 直接注入它，无歧义；
+ 如果以后有了**多个实现**（比如加了 `UserServiceImplCache`）→ Spring 启动时会**报错**（`NoUniqueBeanDefinitionException`，它不知道选哪个），你必须**指定**：给常用的那个标 `**@Primary**`**（默认首选）**，或在注入处 `@Qualifier("userServiceImpl")` 点名。



总结：

准确说法是：**接口让"可替换"成为可能，真正挑哪个由启动时的配置决定，不是自动猜。**

