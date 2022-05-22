# HVALS

---

## 官方参考

[HVALS官方文档参考](https://redis.io/commands/HVALS/)

## 命令语法

> HVALS key 

## 作用

获取指定键对应hash的所有字段的值

## 复杂性

- 时间复杂度

  - O(n), n为hash长度

## 参数

- key

  需要获取字段值hash的键

## 返回结果

- Array reply

  hash字段值列表

## 示例

```bash
HVALS key
```