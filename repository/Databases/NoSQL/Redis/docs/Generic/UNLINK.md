# UNLINK

---

## 官方参考

[UNLINK官方文档参考](https://redis.io/commands/UNLINK/)

## 命令语法

> UNLINK key [key...]

## 作用

类似于[DEL](/repository/Databases/NoSQL/Redis/docs/Generic/DEL.md#DEL), 不同之处在于UNLINK会在不同线程执行内存回收, 是非阻塞的, 而[DEL](/repository/Databases/NoSQL/Redis/docs/Generic/DEL.md#DEL)是阻塞的.

## 复杂性

- 时间复杂度

  - O(n), n为删除的键数量 

## 参数

- key

  需要删除的键

## 返回结果

- Integer reply
  
  被删除键的数量

## 示例

```bash
UNLINK key
```