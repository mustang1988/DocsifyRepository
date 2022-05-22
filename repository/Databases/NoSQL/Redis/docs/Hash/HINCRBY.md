# HINCRBY

---

## 官方参考

[HINCRBY官方文档参考](https://redis.io/commands/HINCRBY/)

## 命令语法

> HINCRBY key field increment 

## 作用

为指定键对应的hash的指定字段值加进行+n操作

如果指定键对应的hash中不包含指定的字段, 则先创建该字段, 并设置值为0, 再进行加进行+n操作

如果指定的键不存在时, 会先创建该键, 并设置指定字段值为0, 再进行加进行+n操作

与[INCRBY](/repository/Databases/NoSQL/Redis/docs/String/INCRBY.md#INCRBY)相同

!> 该操作对数值的范围有限制, 限制为64位带符号整数(-2^63, 2^63-1)

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要执行操作的hash的键

- field

  需要执行+n操作的字段名

- increment

  需要执行的字段增加量

## 返回结果

- Integer reply

  执行+n操作后字段的值

## 示例

```bash
HINCRBY key
```