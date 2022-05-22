# HSET

---

## 官方参考

[HSET官方文档参考](https://redis.io/commands/HSET/)

## 命令语法

> HSET key field value [ field value ...]

## 作用

为指定键对应的hash设置一个或多个字段的值

当指定的键不存在时会先创建一个该键的空hash, 在执行字段值设置

当指定键对应hash中指定字段已经存在, 会使用新的值覆盖原有值

## 复杂性

- 时间复杂度

  - O(n), n为需要设置的字段的数量

## 参数

- key

  需要设置值的hash的键

- field

  需要设置的hash字段名

- value

  需要设置的hash字段值

## 返回结果

- Integer reply

  hash中新增加字段的数量

  !> 注意, 返回的是**新增加**字段的数量, 如果hash中已经存在指定字段, 此时该字段的值会被更新, 但是返回结果会是0

## 示例

```bash
HSET key field1 "hello" field2 "world"
```