---
title: HashMap
url: https://www.yuque.com/ehsuh/oguki0/bqa5qtxg250lc6s1
doc_id: 283767946
exported_at: 2026-09-12T10:02:13
---

```java
Map<String, Integer> ageMap = new HashMap<>();
ageMap.put("张三", 20);
ageMap.put("李四", 25);
System.out.println(ageMap);
```

增 / 改：put(key, value)

尖括号前是键，后是值

如果键已经存在，put 会覆盖旧值（相当于修改）



```java
scores.putIfAbsent("英语", 100); // 英语已经存在，不会改
scores.putIfAbsent("物理", 70);  // 物理不存在，放入
System.out.println("putIfAbsent后：" + scores);
```

注意：HashMap 不保证顺序，输出顺序可能每次不同。



关于putAll

putAll 是 Map 接口自带的一个方法，作用就是把另一个 Map 的所有键值对一次性复制过来，遇到相同的键就覆盖。你第4题用循环遍历 phoneBook2 然后逐个 put 到 phoneBook1，完全正确，而且更底层。putAll 就是把你写的那个循环封装好了：

```java
java
phoneBook1.putAll(phoneBook2);  // 等价于你的循环
```







删：remove(key)  

```java
String removed = capitals.remove("日本");
        System.out.println("被删除的值：" + removed);
        System.out.println("删除后：" + capitals);
```





清空

```java
capitals.clear();
```

capitals.isEmpty()是检验hashmap是否为空的方法





查：get(key)、containsKey、containsValue

```java
int xiaomingAge = ages.get("小明");
        System.out.println("小明的年龄：" + xiaomingAge);
```

如果键不存在，get 返回 null

```java
int xiaoliAge2 = ages.getOrDefault("小李", -1);
        System.out.println("小李的年龄（默认-1）：" + xiaoliAge2);

```



```java
boolean hasXiaohong = ages.containsKey("小红");
        System.out.println("是否包含小红：" + hasXiaohong);
```



```plain
boolean hasAge13 = ages.containsValue(13);
        System.out.println("是否包含年龄13：" + hasAge13);
```



```plain
System.out.println("map 大小：" + ages.size());
```



遍历 HashMap（重点）



遍历有几种方式，常用的是 keySet()、values()、entrySet()。



```plain
for (String name : studentCourses.keySet()) {
            System.out.println("键：" + name);
```



```plain
for (String course : studentCourses.values()) {
            System.out.println("值：" + course);
```



```plain
for (Map.Entry<String, String> entry : studentCourses.entrySet()) {
            String key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + " -> " + value);
```



```java
studentCourses.forEach((name, course) -> {
    System.out.println(name + " 选了 " + course);
```





小结:

创建：new HashMap<>()

· 增/改：put(k, v)

· 删：remove(k)，clear()

· 查：get(k)，getOrDefault(k, default)，containsKey(k)，containsValue(v)

· 遍历：keySet() / values() / entrySet()，推荐 entrySet()。



