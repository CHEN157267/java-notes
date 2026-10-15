---
title: 二、BusinessException 的设计
url: https://www.yuque.com/ehsuh/pggizs/gp3q633ezx3gcsbh
doc_id: 288124399
exported_at: 2026-10-15T19:52:57
---

```plain
public class BusinessException extends RuntimeException {
    private int code;
    public int getCode() { return code; }
    public BusinessException(String message, int code) {
        super(message);      // 把 message 存进父类，e.getMessage() 才取得到
        this.code = code;    // 业务码，最终写进 Result.code
    }
}
```

**① 为什么 **`**extends RuntimeException**`**（unchecked）** 让业务异常"轻装上阵"：抛的人**不用改方法签名**，接的人能接就接、不接就冒泡。

**② 若改成 **`**extends Exception**`**（checked）会多出什么** 编译器**强制处理**：凡是"可能抛它的方法"都要 ① 方法名上写 `throws BusinessException`（一层层上传），或 ② 就地 `try-catch`。Service / Controller **每层都得挂声明**，很啰嗦。

**③ **`**code**`** 给谁用**`new BusinessException("...", 404)` → 冒泡到 `handleBusinessException` → `Result.error(e.getCode(), e.getMessage())` → **写进响应体 **`**Result.code**`。 最关键的一点：**抛异常的人只负责"报告发生了什么"，"变成什么响应"是 handler 的事**——解耦。

**④ **`**super(message)**`** 不写会怎样**`message = null` → 前端只收到 code、没有文字说明。

⚠️ 注意：构造器参数顺序是 `(String message, int code)`，**message 在前**。调用时别写反。

