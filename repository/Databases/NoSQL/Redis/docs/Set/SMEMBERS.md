# SMEMBERS

---

## 官方参考

[SMEMBERS官方文档参考](https://redis.io/commands/SMEMBERS/)

## 命令语法

> SMEMBERS key 

## 作用

获取指定键对应set的所有元素

## 复杂性

- 时间复杂度

  - O(n), n为set的长度

## 参数

- key

  需要获取成员的键

## 返回结果

- Array reply

  set的所有成员

## 示例

```bash
SMEMBERS key
```