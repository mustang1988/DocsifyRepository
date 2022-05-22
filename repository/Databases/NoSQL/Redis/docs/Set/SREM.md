# SREM

---

## 官方参考

[SREM官方文档参考](https://redis.io/commands/SREM/)

## 命令语法

> SREM key member [member ...] 

## 作用

从指定键的set中移除一个或多个成员

如果指定的成员不存在，则不做任何操作

如果指定的键不存在会被认为该键对应的是一个空set，所以不会抛出异常

## 复杂性

- 时间复杂度

  - O(n), n为被移除元素的个数

## 参数

- key

  需要移除成员的set的键

- member

  需要移除的元素, 可以是多个

## 返回结果

- Integer reply

  返回被实际移除元素的个数

  - 0, 指定的键不存在, 或指定的成员不存在时返回

## 示例

```bash
SREM key member1 member2
```