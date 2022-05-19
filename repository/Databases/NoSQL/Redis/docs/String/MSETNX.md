# MSETNX

---

## 官方参考

[MSETNX官方文档参考](https://redis.io/commands/MSETNX/)

## 命令语法

> MSETNX key value [ key value ...] 

## 作用

与[MSET](/repository/Databases/NoSQL/Redis/docs/String/MSET.md)类似, 但是会检查指定的键是否已经存在, 当且仅当所有给定的键都不存在时才会执行存入操作.

## 复杂性

- 时间复杂度

  - O(n), n为指定键值对的数量

## 参数

- key

  需要存入值的键

- value

  需要存入的值

## 返回结果

- Integer reply

    - 1, 所有给定的键均不存在, 并全都存入成功时返回
    - 0, 至少有一个键已经存在, 所有键均没有执行存入时返回

## 示例

```bash
MSETNX key1 value1 key2 value2
```