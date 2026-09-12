---
title: UI设计
url: https://www.yuque.com/ehsuh/oguki0/ff6akngk89xscpuw
doc_id: 217149689
exported_at: 2026-09-12T09:40:15
---

通过·创建JFrame对象·来设定窗口，setVisible是显示设定的窗口

<!-- 这是一张图片，ocr 内容为：好玩 牛逼牛逼 112  00263401 ENATISEL-APAS-ASEG  DJEA  DJEARN S34 !!!!PY! PACKAGE COM.ITHEIMA.UI; IMPORT JAVAX.SWING.*; 团 EDERNALUBRARIES PUBLIC CLASS TEST 5 6 PUBLIC STATIC VOID MAIN(STRING[]ARGS){ 7 /1.创建一个游戏的主界面 JFRAME GAMEJFRAME - NEW JFRAME(); 8 GAMEJFRAME.SETSIZE(WIDTH:603,HEIGHT:680) 10 GAMEJFRAME.SETVISIBLE(TRUE); F,RUN M RODO O PIOBLERAS  BUILD COMPLETED SACCESCFALY IN 2 SEC,104 MS(MOMENTS AGO) 高级软件人才培训专家 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745630958431-9b843943-b2ef-4788-a9b9-8209c8724341.png)



详细

<!-- 这是一张图片，ocr 内容为：PUBLIC CLASS GAMEJFRAME EXTENDS JFRAME //JFRAME界面,窗体 1/子类呢?也表示界面,窗体 //规定:GAMEJFRAME这个界面表示的就是游戏的主界面 1/以后跟游戏相关的所有逻辑都写在这个类中 PUBLIC GAMEJFRAME(){ //设置界面的宽高 THIS.SETSIZE( WIDTH:603,HEIGHT:680); //设置界面的标题 THIS.SETTITLE("拼图单机版V1.0"); //设置界面置顶 THIS.SETALWAYSONTOP(TRUE); //设置界面居中 THIS.SETLOCATIONRELATIVETO(NULL); //设置关闭模式 THIS.SETDEFAULTCLOSEOPERATION(WINDOWCONSTANTS.EXIT_ON_CLOSE); 1/让显示显示出来,建议写在最后 THIS.SETVISIBLE(TRUE); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745631231495-0913ad6e-5df0-49ca-b6ad-06c4111b0b2a.png)

其中这一步中的数字有0到3，

<!-- 这是一张图片，ocr 内容为：THIS.SETDEFAULTCLOSEOPERATION(2); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745633632923-408747ca-df25-497f-b780-84b39d6a86b6.png)

<!-- 这是一张图片，ocr 内容为：什么都不做的默认窗口关闭操作. FINAL CLOSE O ; INT PUBLIC STATIC DO ON NOTHING HIDE-WINDOW默认窗口关闭操作 FINAL INT HIDE ON_CLOSE 1; PUBLIC STATIC DISPOSE-WINDOW默认的窗口关闭操作. 注意:当LAVA虚拟机(VM)中的最后一个可显示窗口被处理掉时,VM可能会终止,有关详细信息,请参 阅AWT线程问题. 也可以看看: JAVA.AWT.WINDOW.DISPOSE(),JINTERNALFRAME.DISPOSE() INT FINAL PUBLIC ON  CLOSE 2 STATIC DISPOSE 退出应用程序默认的窗口关闭操作.尝试在支持此功能的WINDOWS(例女QJFRAME)上设置此功能,可能 会引发基于SECURITYEXCEPTION的SECURITYMANAGER.建议您仅在应用程序中使用它. 自从: 1.4 JFRAME.SETDEFAULTCLOSEOPERATION 也可以看看: FINA1 NT EXIT ON CLOSE INT 3; PUBLIC STATIC 三 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745633732442-9f359e7f-33eb-41ff-88cc-6afdbfdf04e9.png)

输入零：do nothing on close 不做任何事情在关闭的时候（点叉号也没有用）；

一是默认的；

二是当多个窗口都关闭的时候才会停止虚拟机的运行，但是要所有的窗口都做这个定义的时候才会起效；

三代表的是只要关闭其中以的窗口，虚拟机就会关闭；



通过见代码放在不同的类里，能更好的查找代码

<!-- 这是一张图片，ocr 内容为：练习 创建主界面2 用继承改写上述主界面,并思考用继承改写的好处 PUBLIC CLASS LOGINJFRAME EXTENDS 1 NDSJFRAME 1/以后跟登录界面相关的所有代码,都写在这里 PUBLIC CLASS REGISTERJFRAME EXTENDS JFRAME 1/以后跟注册界面相关的所有代码,都写在这里 PUBLIC CLASS GAMEJFRAME EXTENDS JFRAME 1/以后跟游戏界面相关的所有代码,都写在这里 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745631125700-d53efcac-4210-4c07-b733-f0013afdac68.png)





菜单中的各部分名称及其包含关系

<!-- 这是一张图片，ocr 内容为：菜单制作 JMENUBAR JMENU 功能 JMENULTEM 重新游戏 一键通关 JMENULTEM JMENULTEM 退出 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745631307360-2a772010-d019-4ea9-8b9c-eb9287e7f10b.png)

<!-- 这是一张图片，ocr 内容为：JMENUBAR 功能 1,先创建JMENUBAR 重新游戏 2, 再创建]MENU 3,再创建JMENULTEM 6,最后再把JMENUBAR添加到整个JFRAME界面中 4,把JMENULTEM放到JMENU里面 5,把MENU放到JMENUBAR里面 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745631341023-9ff2c60f-995d-4482-be8b-0a8940b95e22.png)



<!-- 这是一张图片，ocr 内容为：JMENUITEM REPLAYITEM : NEW JMENUITEM(TEXT:"重新游戏"); JMENUITEM RELOGINITEM : NEW JMENUITEM(TEXT:"重新登录"); JMENUITEM CLOSEITEM ; NEW JMENUITEM(TEXT:"关闭游戏"); JMENUITEM ACCOUNTITEM - NEW JMENUITEM(TEXT:"公众号"); 1/将每一个选项下面的条目天极爱到选项当中 FUNCTIONJMENU.ADD(REPLAYITEM); FUNCTIONJMENU.ADD(RELOGINITEM); FUNCTIONJMENU.ADD(CLOSEITEM); ABOUTJMENU.ADD(ACCOUNTITEM); 拼图单机版V1.0 拼囤单机版Y1.0 功能 关于我们 关于我们 功能 //将菜单里面的两个选项添加到菜单当中 公众号 更换图片? JMENUBAR.ADD(FUNCTIONJMENU); 重新游戏 重新登录 JMENUBAR.ADD(ABOUTJMENU); 关闭游戏 //给整个界面设置菜单 THIS.SETJMENUBAR(IMENUBAR) 1/让界面显示出来,建议写在最后 THIS.SETVISIBLE(TRUE); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745631506791-5be0c48a-8087-4a84-9119-df6dad341e88.png)







**导入图片**

先找到文件的所在地，让后复制它（整个文件夹），让后在IDEA中选中模块名，control + V

查找地址

<!-- 这是一张图片，ocr 内容为：3.JPG NEW 4JPG X CUT CTRL+X 5.JPG CTRL+C 自 COPY COPY PATH... 7.JP -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745636681634-5c9b4a73-5560-4577-86eb-5ce7a29c5dea.png)

在将地址放到 new ImageIcon（）的括号内；

<!-- 这是一张图片，ocr 内容为：//初始化图片 PRIVATE VOID INITIMAGE() { //创建一个图片IMAGEICON的对象 //创建一个JLABEL的对象(管理容器) JLABELJLABEL ; NEW JLABEL(ICON); //把管理容器添加到界面中 THIS.ADD(JLABEL); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745636813080-703cec7f-91c3-4c52-94b5-955949621b07.png)

图片默认在正中央





图片位置

<!-- 这是一张图片，ocr 内容为：X 拼圈单机版V1.0 功能 JFRAME JFRAMEW JFRAME(); JFRAME.SETSIZE(603,680); IMAGELCONICON1MAGELCON("图片的路径"图片的路径"); JLABELJLABELLNEWJLABEL(ICON1); JFRAME.ADD(JLABEL1); 人 JFRAME.SETVISIBLE(TRUE); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745636928975-1e3d21cb-11a5-4d05-a3e7-5be8a0b33e1b.png)





指定图片的位置一定要在（把管理容器添加到界面中）之前



<!-- 这是一张图片，ocr 内容为：IMAGE//ANIMALLANIMAL3 CON1 - NEW IMAGEICON( FILENAME:"C:) USERS\ MOON (IDEAPRO IMAGEI CON ICON1 PUZZLEGAME //创建一个JLABEL的对象(管理容器) JLABEL JLABEL1 - NEW JLABEL(ICON1); //指定图片位置 JLABEL1.SETBOUNDS( X:0, Y:0,WIDTH:105,HEIGHT:105); //把管理容器添加到界面中 T //THIS.ADD(JLABEL1); THIS.GETCONTENTPANE().ADD(JLABEL1); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745808089951-af7f8355-7570-4f1e-b555-b19f03f46093.png)

<!-- 这是一张图片，ocr 内容为：/取消默认的居中放置,只有取消了才会按照XY轴的形式添加组件 THIS.SETLAYOUT(NULL) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745808164624-db015a1a-80e7-47b9-ade2-fec7a0045537.png)





图中显示的是隐藏的容器，JFrame只是一个大架子，这个隐藏组件才是装载所有组件（图片，文字，按钮，进度条）的

<!-- 这是一张图片，ocr 内容为：拼图单机版V1.0 X 功能 窗体.GETCONTENTPANE()获取我, 把要显示的图片等东西都给我就OK. 如果给我的东西没有特殊要求,我会 默认放到中间位置. SETLAYOUT(NULL) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745808611266-0646571c-2a20-464b-bb09-15e3b60531fe.png)





<!-- 这是一张图片，ocr 内容为：INASEEN SCON - NEN TNABECTS) BLERANE         NOON)  NOON)] NOON) BA3C-CCCCCCE) PU33ERRRE) ERTNAL) ENT //创建一个JLABEL的对象(管理容器) JLABEL JLABEL1 ; NEW JLABEL(ICON1); //指定图片位置 JLABEL1.SETBOUNDS(X:O,Y:0,WIDTH:105,HEIGHT:105); //把管理容器添加到界面中 //THIS.ADD(JLABEL1); THIS.GETCONTENTPANE().ADD(JLABEL1); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745808235125-0e069038-3dc9-43de-9f8f-5e1d5972705c.png)









<!-- 这是一张图片，ocr 内容为：//初始化图片 PRIVATE VOID INITIMAGE() F INT NUMBER 1; //外循环---把内循环重复执峙了4次. FOR (INTI : I < 4; I+++++){ //内循环--.表示在一行添加4张图片 FOR(INT J - 0;J < 4; J++){ 1/创建一个JLABEL的对象(管理容器) //指定图片位置 JLABEL.SETBOUNDS(X:105 * J,Y:105 * I, WIDTH:105, HEIGHT:105); //把管理容器添加到界面中 THIS.GETCONTENTPANE().ADD(JLABEL); /添加一次之后NUMBER需要自增,表示下一次加载后面一张图片 NUMBER++; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1745809451515-026bbf68-b79a-497c-854c-9b5a39cfcc92.png)

将图片路径的数字.jpg改成number.jpg

