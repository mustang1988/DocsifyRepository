# PEXPIRETIME

---

## 官方参考

[PEXPIRETIME官方文档参考](https://redis.io/commands/PEXPIRETIME/)

## 命令语法

> PEXPIRETIME key 

## 作用

获取键过期时间的UNIX时间戳, 单位*毫秒*, 与[EXPIRETIME](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIRETIME.md#EXPIRETIME)类似, 区别在于[EXPIRETIME](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIRETIME.md#EXPIRETIME)返回的时间戳单位为*秒*

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取过期时间戳的键

## 返回结果

- Integer reply:

  键过期时间的UNIX时间戳, 单位 毫秒

  - -1, 当指定的键为设置过期时间时返回
  - -2, 当指定的键不存在时返回

## 示例

```bash
PEXPIRETIME key
```