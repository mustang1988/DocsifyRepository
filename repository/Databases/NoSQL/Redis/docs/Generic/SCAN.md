# SCAN

---

## 官方参考

[SCAN官方文档参考](https://redis.io/commands/SCAN/)

## 命令语法

> SCAN cursor [MATCH pattern] [COUNT count] [TYPE type]

## 作用

迭代数据库键

## 复杂性

- 时间复杂度

  - O(n), n为迭代次数

## 参数

- 

## 返回结果

- 

## 示例

```bash
SCAN key
```