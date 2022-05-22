# HEXISTS

---

## 官方参考

[HEXISTS官方文档参考](https://redis.io/commands/HEXISTS/)

## 命令语法

> HEXISTS key field

## 作用

检查指定键对应的hash中是否包含指定字段

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要检查字段的hash的键

- field

  需要检查的字段

## 返回结果

- Integer reply

  - 1, 指定字段在指定键对应的hash中存在时返回
  - 0, 指定字段在指定键对应的hash中*不存在*或指定键不存在时返回

## 示例

```bash
HEXISTS key field
```