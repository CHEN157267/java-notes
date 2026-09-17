---
title: 控制器autowire UserService 与“多态”的相似之处
url: https://www.yuque.com/ehsuh/pggizs/lpcuogslg7py60gq
doc_id: 285480717
exported_at: 2026-09-17T22:25:41
---

<font style="color:rgba(0, 0, 0, 0.9);">控制器直接 autowire UserService 就像某种多态，</font>**<font style="color:rgba(0, 0, 0, 0.9);">Spring 启动时</font>**<font style="color:rgba(0, 0, 0, 0.9);">会获取符合条件的实现类；如果直接 auto 实现类的话，功能就完全被写死了。</font>

**<font style="color:rgba(0, 0, 0, 0.9);"></font>**

`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserService userService = 某个实现对象</font>**`**<font style="color:rgba(0, 0, 0, 0.9);">，左边接口类型、右边实现对象，这就是多态。注入时 Spring 帮你把"右边"填好了。</font>**

**<font style="color:rgba(0, 0, 0, 0.9);"></font>**

+ <font style="color:rgba(0, 0, 0, 0.9);">如果</font><font style="color:rgba(0, 0, 0, 0.9);"> </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserService</font>`<font style="color:rgba(0, 0, 0, 0.9);"> </font>**<font style="color:rgba(0, 0, 0, 0.9);">只有唯一一个实现</font>**<font style="color:rgba(0, 0, 0, 0.9);">（你现在的情况）→ 直接注入它，无歧义；</font>
+ <font style="color:rgba(0, 0, 0, 0.9);">如果以后有了</font>**<font style="color:rgba(0, 0, 0, 0.9);">多个实现</font>**<font style="color:rgba(0, 0, 0, 0.9);">（比如加了 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">UserServiceImplCache</font>`<font style="color:rgba(0, 0, 0, 0.9);">）→ Spring 启动时会</font>**<font style="color:rgba(0, 0, 0, 0.9);">报错</font>**<font style="color:rgba(0, 0, 0, 0.9);">（</font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">NoUniqueBeanDefinitionException</font>`<font style="color:rgba(0, 0, 0, 0.9);">，它不知道选哪个），你必须</font>**<font style="color:rgba(0, 0, 0, 0.9);">指定</font>**<font style="color:rgba(0, 0, 0, 0.9);">：给常用的那个标 </font>`**<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Primary</font>**`**<font style="color:rgba(0, 0, 0, 0.9);">（默认首选）</font>**<font style="color:rgba(0, 0, 0, 0.9);">，或在注入处 </font>`<font style="color:rgba(0, 0, 0, 0.9);background-color:rgba(0, 0, 0, 0.05);">@Qualifier("userServiceImpl")</font>`<font style="color:rgba(0, 0, 0, 0.9);"> 点名。</font>

<font style="color:rgba(0, 0, 0, 0.9);"></font>

<font style="color:rgba(0, 0, 0, 0.9);">总结：</font>

<font style="color:rgba(0, 0, 0, 0.9);">准确说法是：</font>**<font style="color:rgba(0, 0, 0, 0.9);">接口让"可替换"成为可能，真正挑哪个由启动时的配置决定，不是自动猜。</font>**

