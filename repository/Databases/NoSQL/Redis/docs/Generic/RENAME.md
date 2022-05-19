# RENAME

---

## 官方参考

[RENAME官方文档参考](https://redis.io/commands/RENAME/)

## 命令语法

> RENAME key newkey 

## 作用

重命名键

!> RENAME执行时, 如果newkey已经存在, 则会覆盖原有值, 此时会隐士的执行[DEL](/repository/Databases/NoSQL/Redis/docs/Generic/DEL.md#DEL), 如果被删除的原始值较大, 可能会出现性能问题, 需要注意.

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要重命名的键

- newkey

  重命名为

## 返回结果

- "OK"

当需要重命名的键不存在时抛出错误

## 示例

```bash
RENAME key newkey
```