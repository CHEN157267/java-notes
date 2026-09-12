---
title: JDK8新增的时间相关类
url: https://www.yuque.com/ehsuh/oguki0/vdapsg54legct99z
doc_id: 220070303
exported_at: 2026-09-12T10:38:09
---

<!-- 这是一张图片，ocr 内容为：为什么要学JDK8新增时间相关类呢? 代码层面 安全层面 计算 JDK7:代码麻烦 日期对象 JDK7:多线程环境下会导致数据安全的问题 毫秒值 比较 判断的方法 解决了这个问题 JDK8:简单 JDK8:时间日期对象都是不可变的, 计算时间间隔的方法 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747531849077-9023af76-4cb0-450e-bd73-ce4e02e90d3a.png)

如果想修改时间，它只会创建新的对象





<!-- 这是一张图片，ocr 内容为：JDK8时间 ZONEID:时区 日期格式化类: DATETIMEFORMATTER DATE类 SIMPLEDATEFORMAT 01 02 INSTANT:时间戳 用于时间的格式化和解析 ZONEDATETIME:带时区的时间 ILILLILIIIIII LIILLILLIILLIII DURATION:时间间隔(秒,纳秒) LOCALDATE:年,月,日 日历类: 工具类 CALENDAR 04 03 PERIOD:时间间隔(年,月,日) LOCALTIME:时,分,秒 年,月,日 CHRONOUNIT:时间间隔 LOCALDATETIME: 时,分,秒 (所有单位) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1747532037954-d1e557d2-842e-4464-b13c-496a0b1a101c.png)

