# HGETALL

---

## 官方参考

[HGETALL官方文档参考](https://redis.io/commands/HGETALL/)

## 命令语法

> HGETALL key 

## 作用

获取指定键对应hash的所有字段值

## 复杂性

- 时间复杂度

  - O(n), n为hash的长度

## 参数

- key

  需要获取值的hash的键

## 返回结果

- Array reply

  hash键值数组

## 示例

```bash
HGETALL key
```