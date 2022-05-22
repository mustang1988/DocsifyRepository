# HSETNX

---

## 官方参考

[HSETNX官方文档参考](https://redis.io/commands/HSETNX/)

## 命令语法

> HSETNX key field value

## 作用

与[HSET](/repository/Databases/NoSQL/Redis/docs/Hash/HSET.md#HSET)类似, 但是只在指定的hash字段名不存在时才执行字段值设置, 否则无事发生, 即该命令只会为hash添加字段

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要设置值的hash的键

- field

  需要设置的hash字段名

- value

  需要设置的hash字段值

## 返回结果

- Integer reply

  - 0, 指定的字段在hash中已经存在, 无事发生时返回
  - 1, 指定的字段添加成功时返回

## 示例

```bash
HSETNX key field value
```