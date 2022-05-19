# DEL

---

## 官方参考

[DEL官方文档参考](https://redis.io/commands/del/)

## 命令语法

> DEL key [key...]

## 作用

删除指定键及其值

## 复杂性

- 时间复杂度

  - 当删除多个键时, 时间复杂度为 O(n), n为被删除键的数量
  - 当删除的键对应的值为复杂类型(list, set, sorted set 或 hash)时, 时间复杂度为 O(m), m为对应复杂类型值的长度
  - 当删除的键对应的值为字符串类型, 时间复杂度为 O(1)

## 参数

- key

  需要删除的键

## 返回结果

- Integer reply
  
  被删除键的数量

## 示例

```bash
# 删除单个键
DEL key
# 删除多个键
DEL key1 key2 key3
```