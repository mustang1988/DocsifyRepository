# SINTER

---

## 官方参考

[SINTER官方文档参考](https://redis.io/commands/SINTER/)

## 命令语法

> SINTER key [key ...] 

## 作用

获取多个键对应set内容的交集

## 复杂性

- 时间复杂度

  - O(n*m), n为所有指定集合中最小的集合长度, m为指定的集合数量

## 参数

- key

  可以为一个或多个, 参与交集比对的集合的键

## 返回结果

- Array reply

  所有指定键set的成员交集

## 示例

```bash
SINTER key1 key2
```