# HSTRLEN

---

## 官方参考

[HSTRLEN官方文档参考](https://redis.io/commands/HSTRLEN/)

## 命令语法

> HSTRLEN key field

## 作用

获取指定键对应hash中指定字段值的长度

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值长度的hash的键

- field

  需要获取值长度的hash中的字段名

## 返回结果

- Integer reply

  值的长度
  - 0, 当指定的键不存在或指定的字段在hash中不存在时返回

## 示例

```bash
HSTRLEN key field
```