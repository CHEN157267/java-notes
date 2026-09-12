---
title: BigDecimal
url: https://www.yuque.com/ehsuh/oguki0/lrb0wcxdgr5feor5
doc_id: 218967336
exported_at: 2026-09-12T10:38:12
---

大致与BigInteger这个包装类的方法相同



<!-- 这是一张图片，ocr 内容为：构造方法获取BIGDECIMAL对象 PUBLIC BIGDECIMAL(DOUBLE VAL) BIGDECIMAL(STRING VAL) PUBLIC 静态方法获取BIGDECIMAL对象 STATIC BIGDECIMAL VALUEOF(DOUBLE VAL) PUBLIC -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746843982782-40cb414c-404b-4c9e-b814-e7f3f1675f8a.png)



<!-- 这是一张图片，ocr 内容为：1/1.通过传递DOUBLE类型的小数来创建对象 //细节: 1/这种方式有可能是不精确的,所以不建议使用 EW BIGDECIMAL(VAL:0.01); BIGDECIMALBD1-NEW BD2:NEW BIGDECIMAL(VAL:0.09); BIGDECIMA1 // SYSTEM.OUT.PRINTLN(BD1); //SYSTEM.OUT.PRINTLN(BD2); 1/2.通过传递字符串表示的小数来创建对象 BIGDECIMAL BD3 NEW BIGDECIMAL(VAL:"O.01"); BIGDECIMAL BD4 NEW BIGDECIMAL(VAL:"O.09"); BD5 BD3.ADD(BD4); BIGDECIMA1 SYSTEM.OUT.PRIRLN(BD3); SYSTEM.OUT.PRINTLN(BD4); SYSTEM.OUT.PRINTIN(BD4); -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746843415941-2b80355b-923b-4721-8ea3-09a089c27ee5.png)

<!-- 这是一张图片，ocr 内容为：/3.通过静态方法获取对象 BIGDECIMAL BD6 BIGDECIMAL.VALUEOF(10.0); BIGDECIMAL BD7 BIGDECIMAL.VALUEOF(10.2); SYSTEM.OUT.PRINTLN(BD6 BD7); //细节: 1/1.如果要表示的数字不大,没有超出DOUBLE的取值范围,建议使用静态方法 1/2.如果要表示的数字比较大,超出了DOUBLE的取值范围,建议使用构造方法 //3.如果我们传递的是0~10之同的整数,包含0,包含10.那么方法会返回己经创建好的对家,不会重新NEW -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746843487992-7f15bfc9-7ad2-47e1-92ee-da2ddb434bf3.png)



<!-- 这是一张图片，ocr 内容为：BIGDECIMAL的使用 方法名 说明 获取对象 PUBLIC STATIC BIGDECIMAL VALUEOF(DOUBLE VAL) 加法 PUBLIC BIGDECIMAL VAL) ADD(BIGDECIMAL : BIGDECIMAL SUBTRACT(BIGDECIMAL VAL) 减法 PUBLIC 乘法 PUBLIC BIGDECIMAL MULTIPLY(BIGDECIMAL VAL) .C BIGDECIMAL DIVIDE(BIGDECIMAL VAL) 除法 PUBLICB PUBLIC BIGDECIMAL DIVIDE(BIGDECIMAL VAL,精确几位,舍入模式)除法 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746844564291-c22e4b44-e9b8-4040-9926-6758dc305afe.png)

第一个除法只能计算除的尽的情况



<!-- 这是一张图片，ocr 内容为：//4.除法 BIGDECIMAL BD6 - BD1.DIVIDE(BD2, SCALE:2, ROUNDINGMODE.HALF_UP)I SYSTEM.OUT.PRINTLN(BD6)://3.33 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746844934560-9d304edf-8a66-4dee-b4fb-fae7a0703561.png)

第二个变量是小数点后保留几位，第三个是四舍五入，要以RoundingMode. 来开头



RoundingMode. 后可用：

<!-- 这是一张图片，ocr 内容为：UP:远离零方向舍入的舍入模式 DOWN:向零方向舍入的舍入模式 CEILING:向正无限大方向舍入的舍入模式 FLOOR:向负无限大方向舍入的舍入模式 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746845859988-a9603d13-fb28-4b61-bc31-a6bb03372b25.png)



BigDecimal的储存原理

<!-- 这是一张图片，ocr 内容为：BIGDECIMAL底层存储方式 BIGDECIMAL("O.226"); 1 BD BIGDECIMAL NEW "0.226" 54] 46, 48 50 50 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746845915830-fe324c4f-6a50-4983-8650-62b8986e6791.png)

转化为字节数组（将字符按照ASCII码表转化为数字）





总结：

<!-- 这是一张图片，ocr 内容为：1.BIGDECIMAL的作用是什么? 表示较大的小数和解决小数运算精度失真问题. BIGDECIMAL的对象如何获取? 2. BIGDECIMAL BIGDECIMAL("较大的小数"); BD1 NEW BD2 BIGDECIMAL.VALUEOF(0.1); BIGDECIMAL 3常见操作 加:ADD 减:SUBTRACT 乘:MULTIPLY (四舍五入:ROUNDINGMODE.HALF_UP) 除:DIVIDE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1746845767254-d0ef26bc-e860-4136-af9d-eb71a5d90cfa.png)

