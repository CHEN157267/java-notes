---
title: Wrapper 是什么？
url: https://www.yuque.com/ehsuh/pggizs/kgzqrv1bv2ruckqq
doc_id: 284939003
exported_at: 2026-09-15T10:12:23
---

**<font style="color:rgba(0, 0, 0, 0.86);">Wrapper 就是"条件"</font>**

```java
// updateById：改第5号这个人（按主键）
userMapper.updateById(user);

// update + Wrapper：把所有密码是123456的人，改成abc（按条件批量改）
userMapper.update(null, new UpdateWrapper<User>()
        .eq("password", "123456")      // 条件：密码=123456
        .set("password", "abc"));      // 改成：abc
```

<font style="color:rgba(0, 0, 0, 0.86);">日常"改某一条数据"就是要id，</font>`<font style="color:rgba(0, 0, 0, 0.86);">updateById</font>`<font style="color:rgba(0, 0, 0, 0.86);"> 就够用。Wrapper 是给"</font>**<font style="color:rgba(0, 0, 0, 0.86);">批量改/按条件改</font>**<font style="color:rgba(0, 0, 0, 0.86);">"准备的</font>

