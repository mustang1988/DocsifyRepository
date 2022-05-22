# SMISMEMBER

---

## 官方参考

[SMISMEMBER官方文档参考](https://redis.io/commands/SMISMEMBER/)

## 命令语法

> SMISMEMBER key member [member ...]

## 作用

此为[SISMEMBER](/repository/Databases/NoSQL/Redis/docs/Set/SISMEMBER.md)的扩展命令, [SISMEMBER](/repository/Databases/NoSQL/Redis/docs/Set/SISMEMBER.md)只可以检查单一元素是否为set的成员, SMISMEMBER则可以同时检查多个元素

## 复杂性

- 时间复杂度

  - O(n), n为参与检查的元素个数

## 参数

- key

  需要检索的set的键

- member

  需要检查的元素, 可以是多个

## 返回结果

- Array reply

  每个参与检查的元素的检查结果列表
  - 0, 指定元素不是set的成员
  - 1, 指定元素是set的成员

## 示例

```bash
SMISMEMBER key "hello" "world"
```