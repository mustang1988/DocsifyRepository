# PERSIST

---

## 官方参考

[PERSIST官方文档参考](https://redis.io/commands/PERSIST/)

## 命令语法

> PERSIST key 

## 作用

清除键上记录的过期时间, 将键变为永久有效

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要清除过期时间的键

## 返回结果

- Integer reply

  - 1, 键的过期时间被成功移除后返回
  - 0, 键不存在或键未设置过过期时间时返回

## 示例

```bash
PERSIST key
```