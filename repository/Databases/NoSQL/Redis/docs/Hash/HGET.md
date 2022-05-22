# HGET

---

## 官方参考

[HGET官方文档参考](https://redis.io/commands/HGET/)

## 命令语法

> HGET key field 

## 作用

获取指定键对应hash指定字段的值

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值的hash的键

- field

  需要获取的字段名

## 返回结果

- Bulk string reply

  指定键对应hash中指定字段的值
  - nil, 指定字段在hash中不存在或指定键不存在时返回

## 示例

```bash
HGET key field
```