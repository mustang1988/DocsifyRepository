# INCRBY

---

## 官方参考

[INCRBY官方文档参考](https://redis.io/commands/INCRBY/)

## 命令语法

> INCRBY key increment

## 作用

对指定键的值进行+n操作

类似于[INCR](/repository/Databases/NoSQL/Redis/docs/String/INCR.md), 不同之处在于, [INCR](/repository/Databases/NoSQL/Redis/docs/String/INCR.md)固定+1, 而INCRBY可以指定加的数值

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

需要对值进行+n操作的键

- increment

需要增加的数值

## 返回结果

- Integer reply

执行+n操作后的值

## 示例

```bash
INCRBY key
```