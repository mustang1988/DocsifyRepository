# DECRBY

---

## 官方参考

[DECRBY官方文档参考](https://redis.io/commands/DECRBY/)

## 命令语法

> DECRBY key decrement

## 作用

对指定键的值进行-n操作

类似于[DECR](/repository/Databases/NoSQL/Redis/docs/String/DECR.md), 不同之处在于, [DECR](/repository/Databases/NoSQL/Redis/docs/String/DECR.md)固定-1, 而DECRBY可以指定减的数值

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

需要对值进行-n操作的键

- decrement

需要减少的数值

## 返回结果

- Integer reply

执行-n操作后的值

## 示例

```bash
DECRBY key 5
```