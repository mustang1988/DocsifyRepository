# LSET

---

## 官方参考

[LSET官方文档参考](https://redis.io/commands/LSET/)

## 命令语法

> LSET key index element 

## 作用

修改指定键对应的列表中指定位置的元素

## 复杂性

- 时间复杂度

  - O(n), n为列表长度

## 参数

- key

    需要修改元素的列表的键

- index

    列表中需要修改元素值的索引

- element

    修改为

## 返回结果

- "OK"

## 示例

```bash
LSET key 1 "hahaha"
```