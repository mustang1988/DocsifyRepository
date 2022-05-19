# PEXPIREAT

---

## 官方参考

[PEXPIREAT官方文档参考](https://redis.io/commands/PEXPIREAT/)

## 命令语法

> PEXPIREAT key unix-time-milliseconds [ NX | XX | GT | LT]

## 作用

同[EXPIREAT](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIREAT.md#EXPIREAT), 不同之处在于, [EXPIREAT](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIREAT.md#EXPIREAT)设置的过期时间单位为秒, 而PEXPIREAT设置的过期时间单位为毫秒.

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要设置过期时间的键

- unix-time-milliseconds

  过期的时间戳, 单位 毫秒

- options

  额外参数, 有以下可选值, 默认不指定, 不指定时, 键的过期时间总是会被更新为新的过期时间
  
  > 额外参数从Redis 7.0 起支持

  - NX

    当键当前未设置过期时间, 才为其设置过期时间

  - XX

    当键当前有设置过期时间, 才为其设置新的过期时间

  - GT

    当新设置的过期时间大于当前已经设置的过期时间, 才为其设置新的过期时间

  - LT

    当新设置的过期时间小于当前已经设置的过期时间, 才为其设置新的过期时间

## 返回结果

  - 1, 过期时间成功设置后返回
  - 0, 过期时间未设置后返回, 例如: 键不存在或是键不满足可选参数条件, 被跳过执行

## 示例

```bash
PEXPIREAT key 1555555555005
```