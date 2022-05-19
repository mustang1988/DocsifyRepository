# SET

---

## 官方参考

[SET官方文档参考](https://redis.io/commands/SET/)

## 命令语法

> SET key value [ NX | XX] [GET] [ EX seconds | PX milliseconds | EXAT unix-time-seconds | PXAT unix-time-milliseconds | KEEPTTL]

## 作用

存入键值对, 如果键已经存在, 默认会覆盖原有值

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

    需要存入值的键

- value

    需要存入的值

- 可选参数

    - NX

      当且仅当键不存在时才执行存入
    
    - XX

      当且仅当键已经存在时才执行存入

    - GET

      返回覆盖前的值, 如果存入前键不存在则返回 nil

    - EX seconds

      设置键过期时间, 单位为秒
    
    - PX milliseconds

      设置键过期时间, 单位为毫秒

    - EXAT unix-time-seconds

        设置键过期时间, 值为秒时间戳
    
    - PXAT unix-time-milliseconds

        设置键过期时间, 值为毫秒时间戳
    
    - KEEPTTL

        保留原始值的过期时间

## 返回结果

- Simple string reply

    - "OK", 存入成功时返回
    - nil, 因为使用了可选参数NX或XX导致不符合条件无法存入时返回, 或使用了可选参数GET但原始值并不存在时返回
    - 原始值, 当使用了可选参数GET且原始值存在时返回

## 示例

```bash
SET key "will expire in a minute" EX 60
```