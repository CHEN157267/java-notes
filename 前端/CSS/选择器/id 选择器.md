---
title: id 选择器
url: https://www.yuque.com/ehsuh/bzc31h/wzg018u8ak7g29sk
doc_id: 244442849
exported_at: 2026-09-12T10:36:27
---

<!-- 这是一张图片，ocr 内容为：ID选择器 作用:查找标签,差异化设置标签的显示效果. 场景:ID选择器一般配合JAVASCRIPT使用,很少用来设置CSS样式 步骤: <STYLE> /*定义ID选择器*/ 定义ID选择器#ID名 #RED COLOR: RED; 使用ID选择器标签添加ID名"ID名" 子 </STYLE> <!--使用ID选择器--> 规则: <DIV ID:"RED">这是DIV 标签</DIV> 同一个ID选择器在一个页面只能使用一次 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1762948539833-341a50fb-5a87-4aab-a577-8536cc2c439b.png)



```html
#red {
color: □red;
}
</style>
</head>
<body>
<!--使用 -->
  <div id ="red">div 标签</div>
```



```html
*{
color: □red;
}
```

这样处理是因为这些标签有初始大小，需要利用*{}来清除标签的初始值



