# RENAMENX

---

## 官方参考

[RENAMENX官方文档参考](https://redis.io/commands/RENAMENX/)

## 命令语法

> RENAMENX key 

## 作用

当新键不存在时, 重命名原键到新键

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要重命名的键

- newkey

  重命名为

## 返回结果

- "OK"

当需要重命名的键不存在时抛出错误

## 示例

```bash
RENAMENX key newkey
```