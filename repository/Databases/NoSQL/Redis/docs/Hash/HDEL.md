# HDEL

---

## 官方参考

[HDEL官方文档参考](https://redis.io/commands/HDEL/)

## 命令语法

> HDEL key field [field ...]

## 作用

移除指定键对应hash的一个或多个字段

如果指定的字段在hash中不存在, 将会忽略

如果指定的键不存在, 则视为被操作hash为一个空hash

## 复杂性

- 时间复杂度

  - O(n), n为被移除的字段数量

## 参数

- key

  需要移除字段的hash的键

- field

  需要移除的字段, 可以是多个

## 返回结果

- Integer reply

  被移除的字段数量

## 示例

```bash
HDEL key
```