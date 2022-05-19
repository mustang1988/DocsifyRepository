# SETEX

---

## 官方参考

[SETEX官方文档参考](https://redis.io/commands/SETEX/)

## 命令语法

> SETEX key seconds value 

## 作用

存入键值对并同时设置其过期时间

等价于 先执行 [SET](/repository/Databases/NoSQL/Redis/docs/String/SET.md#SET) 在执行 [EXPIRE](/repository/Databases/NoSQL/Redis/docs/Generic/EXPIRE.md#EXPIRE), 但不同点在于, SETEX 是一个原子操作

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

    需要存入值的键

- seconds

    过期时间, 单位为秒

- value

    需要存入的值

## 返回结果

- "OK"

## 示例

```bash
SETEX key 10 value
```