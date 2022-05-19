# KEYS

---

## 官方参考

[KEYS官方文档参考](https://redis.io/commands/KEYS/)

## 命令语法

> KEYS pattern

## 作用

查询所有符合规则的键

!> 非常不建议在生产环境等重要环境中使用该命令, 会导致性能问题, 该命令只应用于开发和调试, 如果在生产环境有在数据库中大量查询键的需求, 请使用[SCAN](/repository/Databases/NoSQL/Redis/docs/Generic/SCAN.md#SCAN)或其他命令代替.

## 复杂性

- 时间复杂度

  - O(n), n为数据库中符合给定规则的键的数量, 弱未指定规则, n就是当前数据库中所有键的数量

## 参数

- pattern

  键匹配规则

  配规则示例:
  - h?llo, 匹配:hello, hallo, hxllo
  - h*llo, 匹配: hllo, heeeello
  - h[ae]llo, 匹配: hello ,hallo, 但不匹配: hillo
  - h[^e]llo, 匹配: hallo, hbllo, ..., 但不匹配: hello
  - h[a-b]llo, 匹配: hallo, hbllo

## 返回结果

- Array reply

  匹配规则要求的键列表

## 示例

```bash
KEYS helloworld
```