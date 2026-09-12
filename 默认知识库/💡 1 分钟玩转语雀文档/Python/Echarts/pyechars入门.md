---
title: pyechars入门
url: https://www.yuque.com/ehsuh/oguki0/oi4anpmsixvg71u9
doc_id: 245419598
exported_at: 2026-09-12T10:05:59
---

```python
#导包，导入Line功能构建折线图对象
from pyecharts.charts import Line
# 得到折线图对象
line = Line()
# 添加x轴数据
1ine.add_xaxis([“中国”，“美国”，“英国”])
# 添加y轴数据
1ine.add_ yaxis("gdp",[30, 20 ,10])
10 #生成图表
11 line.render()
```



1.pyecharts模块中有很多的配置选项,常用到三个类别的选项:全局配置选项系列配置选项

2.全局配置项能做什么?

配置图表的标题

配置图例。

配置鼠标移动效果

配置工具栏

等整体配置项

