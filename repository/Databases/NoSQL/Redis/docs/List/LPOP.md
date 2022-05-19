# LPOP

---

## 官方参考

[LPOP官方文档参考](https://redis.io/commands/LPOP/)

## 命令语法

> LPOP key [count]

## 作用

从指定键的列表前端移除1个或多个元素

## 复杂性

- 时间复杂度

  - O(n), n为移除的元素个数

## 参数

- key

    需要移除元素的列表的键

- count

    需要移除的元素个数, 可选参数, 默认值为1

## 返回结果

- Bulk string reply

    当未指定count参数时返回被移除的元素
    
    - nil, 当指定的键不存在时返回

- Array reply

    当指定count参数时返回被移除的元素列表

    - nil, 当指定的键不存在时返回

## 示例

```bash
# 移除列表中的第一个元素
LPOP key
# 移除列表中的前两个元素
LPOP key 2
```