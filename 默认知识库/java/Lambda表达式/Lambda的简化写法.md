---
title: Lambda的简化写法
url: https://www.yuque.com/ehsuh/oguki0/sqwpq6fc6bxfwq9t
doc_id: 222095242
exported_at: 2026-09-12T10:07:09
---



<!-- 这是一张图片，ocr 内容为：LAMBDA的省略规则: 1.参数类型可以省略不写. 2.如果只有一个参数,参数类型可以省略,同时()也可以省略. 3.如果LAMBDA表达式的方法体只有一行,大括号,分号,RETURN可以省略不写,需要同时省略 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1748832637966-bc9f4773-5940-4d7c-8bd1-28db0283b6f5.png)<!-- 这是一张图片，ocr 内容为：INTEGER[] ARR 三{2, 3,1, 5,6, 7,8, 4, 4, 9}; U COMPARATOR<INTEGER>() ARRAYS.SORT(ARR, NEW COM @OVERRIDE PUBLIC INT COMPARE(INTEGER O1, 02){ INTEGER 02; RETURN O1 子); //LAMBDA完整格式 ARRAYS.SORT(ARR, (INTEGER OL, INTEGER O2) -> { 02; RETURN O1 - O //1AMBDA省略写法 ARRAYS.SORT(ARR, (O1, 02) -> 01 - O2); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1748832580123-0a7801a7-1043-420d-abeb-385cff3b646f.png)



<!-- 这是一张图片，ocr 内容为：LAMBDA表达式的省略写法 省略核心:可推导,可省略 参数类型可以省略不写. 如果只有一个参数,参数类型可以省略,同时()也可以省略. 如果LAMBDA表达式的方法体只有一行, 大括号,分号,RETURN可以省略不写,需要同时省略. -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1748832736346-50695004-4146-4112-9648-d1caee43c82b.png)



简单用例

```plain
package com.c;

import java.util.Arrays;
import java.util.Comparator;

public class test {
    public static void main(String[] args) {
        String[] arr = {"a","aaaa", "aaa","aa"};
        Arrays.sort(arr, (o1, o2)-> o1.length() - o2.length());
        System.out.println(Arrays.toString(arr));
    }

}

```

