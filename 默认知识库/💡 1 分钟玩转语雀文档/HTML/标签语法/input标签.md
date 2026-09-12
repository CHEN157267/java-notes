---
title: input标签
url: https://www.yuque.com/ehsuh/oguki0/nmpcsb3c7rttceak
doc_id: 244338954
exported_at: 2026-09-12T10:05:29
---

<!-- 这是一张图片，ocr 内容为：INPUT 标签基本使用 INPUT 标签 TYPE 属性值不同,则功能不同. <INPUT TYPE">.."> 说明 TYPE属性值 文本框,用于输入单行文本 TEXT 密码框 PASSWORD 单选框 RADIO CHECKBOX 多选框 上传文件 FILE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762864687259-2ee95a0d-6dcb-4ee9-a5ae-28642ecc8672.png)

```html
<!-- 特点:输入什么就显示什么 --》文本框:
<input type="text”><br><br》
<!-- 特点:输入什么都是以点的形式显示-->密码框:
<input type="password">
<br>
<br>
单选框:<input type="radio">
<br>
<br>
多选框:<input type="checkbox"><br><br>
上传文件:<input type="file”>
```



<!-- 这是一张图片，ocr 内容为：INPUT标签占位文本 占位文本:提示信息. <INPUTTYPE"..."PLACEHOLDER:"提示信息"> 登录 注册 文本框和密码框都可以使用. 邮箱/手机号码/小米ID 密码 已间读并同意小米帐号用户协议和隐私政策 登录 手机号登录 忘记密码? 其他方式登录 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762930821348-6937a9c2-50c5-4c1c-8533-bd004d87ab1c.png)

```html
<input type=".." placeholder="提示信息">
```



单选框radio

<!-- 这是一张图片，ocr 内容为：单选框 RADIO 常用属性: 作用 属性名 特殊说明 控件分组,同组只能选中一个(单选功能) 控件名称 NAME 男 O女 我是 属性名和属性值相同,简写为一个单词 默认选中 CHECKED 男 "GENDER" CHECKED>男 <INPUT TYPE"RADIO NAME- 女 <INPUT TYPE"RADIO" NAMEGENDER -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762930878913-f51eb269-ea59-404e-8628-7f1978d25959.png)

```html
<input type="radio"name="gender">男
<input type="radio"name="gender" checked>女
```

checked（用户未填写时，默认值）



上传多个文件

<!-- 这是一张图片，ocr 内容为：上传文件-FILE 默认情况下,文件上传表单控件只能上传一个文件,添加MULTIPLE属性可以实现文件多选功能. <INPUT TYPE"FILE"MULTIPLE> -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762930976874-c5aaa6fe-b4d8-499e-ac9a-ad21aca6b3f1.png)

```html
<input type="file" multiple>
```



多选的默认选中

```html
兴趣爱好: 
<input type="checkbox"> 敲代码
<input type="checkbox" checked>敲前端代码" checkied
<input type="checkbox">敲前端 HTML 代码
```



下拉菜单

<!-- 这是一张图片，ocr 内容为：城市: 北京 城市: 北京 北京 上海 广州 深圳 武汉 标签:SELECT嵌套OPTION,SELECT是下拉菜单整体,OPTION是下拉菜单的每一项. <SELECT> <OPTION>北京</OPTION> <OPTION>上海</OPTION> <OPTION>广州</OPTION> <OPTION>深圳</OPTION> 武汉</OPTION> <OPTIONSELECTED> -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931216199-c89449bd-3ccb-4426-94f3-90f72419816b.png)



input构建文本域

```html
<textarea>请输入评论</textarea>
```



<!-- 这是一张图片，ocr 内容为：LABEL 标签 作用:网页中,某个标签的说明文本. 手机号码 中国大陆 请输入你的手机号码 +86 验证码 获取验证码 请输入校验码 注册 经验:用LABEL标签绑定文字和表单控件的关系,增大表单控件的点击范围. O女 我是 男 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931443186-23715b5d-d6dc-403f-9a93-cbf33b3b3189.png)

就是增大了咱们表单控件的点击范围

```html
# 简洁写法
<label><input type="radioname="gender">女</label>

# 常规写法
<input type="radio" name="gender" id ="man"> <label for="man">男</label>
```

<!-- 这是一张图片，ocr 内容为：LABEL标签-增大点击范围 写法一 LABEL 标签只包裹内容,不包裹表单控件 设置LABEL 标签的 属性值和表单控件的ID属性值相同 <INPUT TYPE"RADIO"ID"ID"MAN"> <LABEL FOR"MAN">男</LABEL> 写法二 使用LABEL标签包裹文字和表单控件,不需要属性 <LABEL><INPUT TYPE"RADIO">女</LABEL> -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931804159-73936415-63c9-4336-98c2-fc0a69e1cb53.png)



button

<!-- 这是一张图片，ocr 内容为：按钮-BUTTON <BUTTON TYPE`>按钮</BUTTON> TYPE属性值: 说明 TYPE属性值 提交按钮,点击后可以提交数据到后台(默认功能) SUBMIT 重置按钮,点击后将表单控件恢复默认值 RESET 普通按钮,默认没有功能,一般配合JAVASCRIPT使用 BUTTON -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931818914-62eca95e-9149-4fd5-85a1-1b94e5b4f52d.png)

```html
<button type="submit”>提交</button>
<button type="reset">重置</button>
<button type="button”>普通按钮</button>
```



<!-- 这是一张图片，ocr 内容为：无语义的布局标签 作用:布局网页(划分网页区域,摆放内容) DIV:独占一行 SPAN:不换行 <DIV>DIV标签,独占一行</DIV> <SPAN>SPAN 标签,不换行</SPAN> -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931900211-eeaf0ed8-f7ce-4551-97f3-9ffc08bf9ff5.png)



<!-- 这是一张图片，ocr 内容为：字符实体 作用:在网页中显示预留字符. 显示结果 描述 实体名称 空格 &NBSP; 小于号 &LT; 大于号 &GT; -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762931915498-f4b1a2c1-d8d9-4709-ad24-56189fdfc556.png)

```html
乾坤未定，你我皆是黑&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;马
&lt;p&gt;
```

