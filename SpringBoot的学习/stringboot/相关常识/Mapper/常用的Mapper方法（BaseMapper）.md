---
title: 常用的Mapper方法（BaseMapper）
url: https://www.yuque.com/ehsuh/pggizs/mgfkgksv5wa0gq84
doc_id: 285995985
exported_at: 2026-09-21T20:48:34
---

**查询**

| **方法** | **用途** | **返回** |
| --- | --- | --- |
| `selectById(id)` | 按主键查一条 | 实体 / null |
| `selectList(wrapper)` | 按条件查多条，传 `null`<br/> = 全表 | `List` |
| `selectCount(wrapper)` | 数条数 | `Long` |
| `exists(wrapper)` | 存不存在 | `boolean` |
| `selectOne(wrapper)` | 按条件查**一条**（查到多条会抛异常） | 实体 / null |
| `selectPage(page, wrapper)` | 分页（要装分页插件） | `IPage` |


**新增**：`insert(entity)` → 影响行数，**并回填主键**  
**修改**：`updateById(entity)` 按主键改 / `update(entity, wrapper)` 按条件改  
**删除**：`deleteById(id)` / `delete(wrapper)` / `deleteBatchIds(ids)` 批量

