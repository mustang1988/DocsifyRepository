# SUNIONSTORE

---

## 官方参考

[SUNIONSTORE官方文档参考](https://redis.io/commands/SUNIONSTORE/)

## 命令语法

> SUNIONSTORE destination key [key ...] 

## 作用

此为[SUNION](/repository/Databases/NoSQL/Redis/docs/Set/SUNION.md)的扩展命令, [SUNION](/repository/Databases/NoSQL/Redis/docs/Set/SUNION.md)会直接返回合集的结果, SUNIONSTORE 则可以将合集结果存储到指定的键中

## 复杂性

- 时间复杂度

  - O(n), n为指定键对应set中成员的总数

## 参数

- destination

  用于存储合集结果的键

- key

  进行合集操作的set的键, 可以是多个

## 返回结果

- Integer reply

  合集结果的长度

## 示例

```bash
SUNIONSTORE destination key1 key2 key3
```