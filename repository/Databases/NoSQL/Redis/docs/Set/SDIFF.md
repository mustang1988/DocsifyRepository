# SDIFF

---

## 官方参考

[SDIFF官方文档参考](https://redis.io/commands/SDIFF/)

## 命令语法

> SDIFF key [key ...]

## 作用

获取指定键对应set与其他一个获多个键对应set的差集

## 复杂性

- 时间复杂度

  - O(n), n为所有参与差集比对的set中成员的数量

## 参数

- key

  需要进行差集比对的基set的键

- [key...]

  需要进行差集比对的其他set的键

## 返回结果

- Array reply

  差集比对结果, 结果为仅在第一个参数键对应set中出现, 但在其他所有指定键的set中均未出现的成员组成的列表
  例如
  ```bash
  key1 = {a,b,c,d}
  key2 = {c}
  key3 = {a,c,e}
  SDIFF key1 key2 key3 = {b,d}
  ```

## 示例

```bash
SDIFF key1 key2
```