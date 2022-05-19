# LTRIM

---

## 官方参考

[LTRIM官方文档参考](https://redis.io/commands/LTRIM/)

## 命令语法

> LTRIM key start stop 

## 作用

裁剪指定键对应的列表, 只保留指定索引范围内的元素

## 复杂性

- 时间复杂度

  - O(n), n为列表中被移除元素的个数

## 参数

- key

    需要裁剪元素的列表的键

- start

    裁剪起始点索引

- stop

    裁剪结束点索引

## 返回结果

- "OK"

## 示例

```bash
LTRIM key
```