# SDIFFSTORE

---

## 官方参考

[SDIFFSTORE官方文档参考](https://redis.io/commands/SDIFFSTORE/)

## 命令语法

> SDIFFSTORE destination key [key ...] 

## 作用

此命令为[SDIFF](/repository/Databases/NoSQL/Redis/docs/Set/SDIFF.md)的扩展命令, 不同点在于, [SDIFF](/repository/Databases/NoSQL/Redis/docs/Set/SDIFF.md)会直接返回差集结果, SDIFFSTORE则会将差集结果存储到redis中

!> 如果在SDIFFSTORE中指定的存储差集结果的键存在, 会直接覆盖原有的值

## 复杂性

- 时间复杂度

  - O(n), n为所有参与差集比对的set中成员的数量

## 参数

- key

  需要进行差集比对的基set的键

- destination

  用于存储差集结果的键

- [key...]

  需要进行差集比对的其他set的键

## 返回结果

- Integer reply

  差集结果的长度

## 示例

```bash
# 找出key1 set中所有元素, 均为出现在 key2,key3和key4的元素组成新的set, 存入result中
SDIFFSTORE result key1 key2 key3 key4
```