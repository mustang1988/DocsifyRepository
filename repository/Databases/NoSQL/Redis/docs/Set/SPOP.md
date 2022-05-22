# SPOP

---

## 官方参考

[SPOP官方文档参考](https://redis.io/commands/SPOP/)

## 命令语法

> SPOP key [count]

## 作用

从指定键的set中*随机*获取一个或多个元素, 并将它们从set中移除

## 复杂性

- 时间复杂度

  - O(n), n为指定的元素个数

## 参数

- key

  需要执行操作set的键

- count

  需要获取的元素个数的上限, 可选, 默认值: 1, 实际获取的元素个数由被操作的set长度决定

## 返回结果

- Bulk string reply

  当未指定count参数时返回

  被移除的元素
  - nil, 当指定的键不存在时返回

- Array reply

  指定了count参数时返回

  被移除的元素列表

  当指定的键不存在时返回空列表

## 示例

```bash
SPOP key
```