# SUNION

---

## 官方参考

[SUNION官方文档参考](https://redis.io/commands/SUNION/)

## 命令语法

> SUNION key [key ...] 

## 作用

获取指定多个键对应set的合集

## 复杂性

- 时间复杂度

  - O(n), n为指定键对应set中成员的总数

## 参数

- key

  进行合集操作的set的键, 可以是多个

## 返回结果

- Array reply

  合集结果列表

## 示例

```bash
SUNION key1 key2 key3
```