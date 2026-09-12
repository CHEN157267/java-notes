---
title: (dict)字典
url: https://www.yuque.com/ehsuh/oguki0/yk2dbkgmrn7e0gzp
doc_id: 242082896
exported_at: 2026-09-12T10:06:10
---

<!-- 这是一张图片，ocr 内容为：不过存储的元素是一个个的:键值对,如下语法 字典的定义,同样使用 #定义字典字面量 FKEY:VALUEGKEY:VALUE, :VALUE KEY: 3#定义字典变量 CT : KEY:VALUE, KEY:VALUE,............. KEY:VALUE; 4 MYDICT #定义空字典 5 6 #空字典定义方式1 MY-DICT DICT() 7 #空字典定义方式2 MYDICT -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1761482956134-13199ec8-8142-4c34-89a5-4820f207289d.png)



字典同集合一样，不可以使用下标索引

但是字典可以通过Key值来取得对应的Value。

键（Key）是不能重复的，而值（Value）则可以重复 。

```java
 # 语法，字典[Key]可以取到对应的Value
stu_score={"王力鸿":99，"周杰轮":88,"林俊节”:77} 
print(stu_score["王力鸿"])# 结果99
print(stu_score["周杰轮"])#结果88
print(stu_score["林俊节”])十#结果77
```

<!-- 这是一张图片，ocr 内容为：字典的KEY和VALUE可以是任意数据类型 (KEY不可为字典) -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1761483140003-bc405540-7a67-4f41-8b08-c1c8c511d9d0.png)



总结：

<!-- 这是一张图片，ocr 内容为：1.为什么使用字典 字典可以提供基于KEY检索VALUE的场景实现 就像查字典一样 1077X 587 PX 2.字典的定义语法 定义字典字面量 {KEY:VALUE,KEY:VALUE, KEY:VALUEJ #定义字典变量 {KEY:VALUE,KEY:VALUE,.............KEY:VALUE} MY-DICT 5#定义空字典 #空字典定义方式1 6MY-DICT #空字典定义方式2 DICT() MY-DICT 3.字典的注意事项 键值对的KEY和VALUE可以是任意类型(KEY不可为字典) 字典内KEY不允许重复,重复添加等同于覆盖原有数据 字典不可用下标索引,而是通过KEY检索VALUE -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1761483157839-a92d01f0-88b5-4775-ac70-d74dc3501964.png)



总结

<!-- 这是一张图片，ocr 内容为：1.字典的常用操作 字典[KEY] 获取指定KEY对应的VALUE值 字典[KEY]VALUE 添加或更新键值对 字典.POP(KEY) 取出KEY对应的VALUE并在字典内删除此KEY的键值对 清空字典 字典.CLEAR() 字典.KEYS() 获取字典的全部KEY,可用于FOR循环遍历字典 计算字典内的元素数量 LEN(字典) 2.操作注意 新增和更新元素的语法一致,如果KEY不存在即新增,如果KEY存在 即更新(KEY不可重复) 3.字典的特点 可以容纳多个数据 可以容纳不同类型的数据 每一份数据是KEYVALUE键值对 可以通过KEY获取到VALUE,KEY不可重复(重复会覆盖) OKTOK (增加或删除更新元素等) 可以修改 支持FOR循环,不支持WHILE循环 吉 1亿 -->
![](https://cdn.nlark.com/yuque/0/2025/png/52131016/1761483524292-74c402af-b180-46c7-8e0b-3ecec1ad2d1c.png)

