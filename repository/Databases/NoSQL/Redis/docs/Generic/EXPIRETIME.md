# EXPIRETIME

---

## 官方参考

[EXPIRETIME官方文档参考](https://redis.io/commands/EXPIRETIME/)

## 命令语法

> EXPIRETIME key 

## 作用

获取键过期时间的UNIX时间戳, 单位 秒

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取过期时间戳的键

## 返回结果

- Integer reply:

  键过期时间的UNIX时间戳, 单位 秒

  - -1, 当指定的键为设置过期时间时返回
  - -2, 当指定的键不存在时返回

## 示例

```bash
EXPIRETIME key
```