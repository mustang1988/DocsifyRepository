# HMGET

---

## 官方参考

[HMGET官方文档参考](https://redis.io/commands/HMGET/)

## 命令语法

> HMGET key field [field ...] 

## 作用

获取指定键对应hash的一个或多个字段的值

## 复杂性

- 时间复杂度

  - O(n), n为指定的字段名的数量

## 参数

- key

  需要获取值的hash的键

- field

  需要获取的hash字段名, 可以是多个

## 返回结果

- Array reply

  hash字段名, 字段值列表

  - nil, 指定的字段不存在或指定的键不存在时返回

## 示例

```bash
HMGET key field1 field2
```