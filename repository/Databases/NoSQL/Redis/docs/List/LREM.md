# LREM

---

## 官方参考

[LREM官方文档参考](https://redis.io/commands/LREM/)

## 命令语法

> LREM key count element 

## 作用

从指定键的列表中按指定方向移除指定数量的指定元素

## 复杂性

- 时间复杂度

  - O(n+m), n 为列表长度, m为被移除元素的个数

## 参数

- key

    需要移除元素的列表的键

- count

    移除的元素个数与移除方向
    - count > 0 时, 列表从前往后检索指定元素, 移除 count 个
    - count < 0 时, 列表从后往前检索指定元素, 移除 |count| 个
    - count = 0 时, 移除列表中所有指定元素

- element

    需要移除元素的值

## 返回结果

- Integer reply

    返回*实际*被移除元素的个数

## 示例

```bash
# 从前往后, 移除列表key中前8个元素a
LREM key 8 a
# 从后往前, 移除列表key中后4个元素b
LREM key -4 b
# 移除列表key中所有的元素c
LREM key 0 c
```