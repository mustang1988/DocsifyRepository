# SINTERSTORE

---

## 官方参考

[SINTERSTORE官方文档参考](https://redis.io/commands/SINTERSTORE/)

## 命令语法

> SINTERSTORE destination key [key ...] 

## 作用

此命令为[SINTE](/repository/Databases/NoSQL/Redis/docs/Set/SINTE.md)的扩展命令, 不同点在于, [SINTE](/repository/Databases/NoSQL/Redis/docs/Set/SINTE.md)会直接返回交集结果, SINTERSTORE则会将差集结果存储到redis中

!> 如果在SINTERSTORE中指定的存储交集结果的键存在, 会直接覆盖原有的值

## 复杂性

- 时间复杂度

  - O(n*m), n为所有指定集合中最小的集合长度, m为指定的集合数量

## 参数

- key

  可以为一个或多个, 参与交集比对的集合的键

- destination

  用于存储交集结果的键

## 返回结果

- Integer reply

  存储的交集set的长度

## 示例

```bash
SINTERSTORE result key1 key2
```