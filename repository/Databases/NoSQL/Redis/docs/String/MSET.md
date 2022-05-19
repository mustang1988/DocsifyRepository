# MSET

---

## 官方参考

[MSET官方文档参考](https://redis.io/commands/MSET/)

## 命令语法

> MSET key value [ key value ...] 

## 作用

批量存入多个键值对

!> 当指定的键存在时, 会覆盖其原有值

?> MSET是原子操作, 所有给定的键值对是一起存入的

## 复杂性

- 时间复杂度

  - O(n), n为指定键值对的数量

## 参数

- key

  需要存入值的键

- value

  需要存入的值

## 返回结果

- "OK"

## 示例

```bash
MSET key1 value1 key2 value2
```