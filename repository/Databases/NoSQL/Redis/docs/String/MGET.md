# MGET

---

## 官方参考

[MGET官方文档参考](https://redis.io/commands/MGET/)

## 命令语法

> MGET key [key ...]

## 作用

批量获取多个键对应的值

## 复杂性

- 时间复杂度

  - O(n), n为指定键的数量

## 参数

- key

  需要获取值的键, 支持多个

## 返回结果

- Array reply

  指定键对应值的列表, 顺序与指定的多个键的顺序一致

  当指定的多个键中有不存在的, 或者其值不是字符串类型的, 则返回的值为*nil*

## 示例

```bash
MGET key1 key2 key3
```