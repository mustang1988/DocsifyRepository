# HKEYS

---

## 官方参考

[HKEYS官方文档参考](https://redis.io/commands/HKEYS/)

## 命令语法

> HKEYS key 

## 作用

获取指定键对应hash的所有字段名

## 复杂性

- 时间复杂度

  - O(n), n为hash长度

## 参数

- key

  需要获取字段名hash的键

## 返回结果

- Array reply

  hash字段名列表

## 示例

```bash
HKEYS key
```