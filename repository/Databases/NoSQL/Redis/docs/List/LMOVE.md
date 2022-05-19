# LMOVE

---

## 官方参考

[LMOVE官方文档参考](https://redis.io/commands/LMOVE/)

## 命令语法

> LMOVE source destination LEFT | RIGHT LEFT | RIGHT

## 作用

从一个列表移动最前/后的1个元素到另一个列表的最前/后的位置处

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- source

    移出元素的列表键

- destination

    移入元素的列表键

- LEFT | RIGHT

    从移除元素列表的最前/后移出1个元素

- LEFT | RIGHT

    将移出的元素放入目标列表的最前/后的位置

## 返回结果

- Bulk string reply

  被移动的元素

## 示例

```bash
# 将 mylist 列表的最后一个元素移动到 myotherlist 列表的第一个位置
LMOVE mylist myotherlist RIGHT LEFT
```