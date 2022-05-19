# EXPIREAT

---

## 官方参考

[EXPIREAT官方文档参考](https://redis.io/commands/EXPIREAT/)

## 命令语法

> EXPIREAT key unix-time-seconds [ NX | XX | GT | LT]

## 作用

类似[EXPIRE](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIRE.md#EXPIRE)的作用, 为键设置过期时间, 不同于[EXPIRE](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIRE.md#EXPIRE), EXPIREAT是将过期时间设置到某个指定的时间戳, 当系统时间到达此时间戳时, 会将键进行删除.

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要设置过期时间的键

- unix-time-seconds

  过期的时间戳, 单位 秒

- options

  额外参数, 有以下可选值, 默认不指定, 不指定时, 键的过期时间总是会被更新为新的过期时间
  - NX

    当键当前未设置过期时间, 才为其设置过期时间

  - XX

    当键当前有设置过期时间, 才为其设置新的过期时间

  - GT

    当新设置的过期时间大于当前已经设置的过期时间, 才为其设置新的过期时间

  - LT

    当新设置的过期时间小于当前已经设置的过期时间, 才为其设置新的过期时间

## 返回结果

- Integer reply

  - 1, 过期时间成功设置后返回
  - 0, 过期时间未设置后返回, 例如: 键不存在或是键不满足可选参数条件, 被跳过执行

## 示例

```bash
# 设置键的过期时间为2011-01-01 00:00:00
EXPIREAT key 1293840000
```