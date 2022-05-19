# PSETEX

---

## 官方参考

[PSETEX官方文档参考](https://redis.io/commands/PSETEX/)

## 命令语法

> PSETEX key milliseconds value 

## 作用

与[SETEX](/repository/Databases/NoSQL/Redis/docs/String/SETEX.md)很类似, 但区别在于设置的过期时间单位为毫秒

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

    需要存入值的键

- milliseconds

    过期时间, 单位为毫秒

- value

    需要存入的值

## 返回结果

- "OK"

## 示例

```bash
PSETEX key 10 value
```