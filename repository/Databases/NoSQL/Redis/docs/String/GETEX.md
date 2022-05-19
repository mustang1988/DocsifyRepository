# GETEX

---

## 官方参考

[GETEX官方文档参考](https://redis.io/commands/GETEX/)

## 命令语法

> GETEX key [ EX seconds | PX milliseconds | EXAT unix-time-seconds | PXAT unix-time-milliseconds | PERSIST] 

## 作用

与[GET](/repository/Databases/NoSQL/Redis/docs/String/GET.md)类似, 获取指定键对应的值, 但同时支持对键设置过期时间

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值的键

- options

  可选参数
  - EX seconds

      设置键在指定seconds秒后过期

  - PX milliseconds

      设置键在指定milliseconds毫秒后过期

  - EXAT unix-time-seconds

      设置键在unix-time-seconds秒对应的时间过期

  - PXAT unix-time-milliseconds

      设置键在unix-time-milliseconds毫秒对应的时间过期

  - PERSIST

      移除当前键的过期时间设置

## 返回结果

- Bulk string reply
  
  键对应的字符串值

  - nil, 当指定的键不存在时返回

## 示例

```bash
GETEX key PERSIST
```