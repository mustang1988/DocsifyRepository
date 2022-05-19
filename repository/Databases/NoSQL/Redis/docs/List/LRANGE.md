# LRANGE

---

## 官方参考

[LRANGE官方文档参考](https://redis.io/commands/LRANGE/)

## 命令语法

> LRANGE key start stop 

## 作用

获取指定键的列表中指定索引范围内的的元素

## 复杂性

- 时间复杂度

  - O(s+n), s为检索起始索引, n为需要返回的元素个数

## 参数

- key

    需要获取元素的列表的键

- start

    检索起始索引

- stop

    检索结束索引

## 返回结果

- Array reply

    指定索引范围内的元素组成的数组

    - 当start索引越界, 返回空数组
    - 当stop索引越界, 会返回列表的所有元素

## 示例

```bash
LRANGE key
```