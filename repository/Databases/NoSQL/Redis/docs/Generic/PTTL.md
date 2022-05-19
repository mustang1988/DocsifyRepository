# PTTL

---

## 官方参考

[PTTL官方文档参考](https://redis.io/commands/PTTL/)

## 命令语法

> PTTL key 

## 作用

类似[TTL](/repository/Databases/NoSQL/Redis/docs/Generic/TTL.md#TTL), 获取指定键的剩余过期时间, 区别在于PTTL返回的剩余过期时间单位为*毫秒*

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取剩余过期时间的键

## 返回结果

- Integer reply

  键的剩余过期时间, 单位 毫秒

  - -2, 指定的键不存在时返回
  - -1, 指定的键存在, 但尚未设置过期时间时返回

## 示例

```bash
PTTL key
```