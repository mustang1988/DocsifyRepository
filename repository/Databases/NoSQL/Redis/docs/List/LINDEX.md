# LINDEX

---

## 官方参考

[LINDEX官方文档参考](https://redis.io/commands/LINDEX/)

## 命令语法

> LINDEX key index 

## 作用

获取指定键列表中指定索引位置的元素

当指定的键对应的值不是列表类型时, 抛出异常

## 复杂性

- 时间复杂度

  - O(n), n为指定的索引与列表边缘的距离, 当指定的索引为列表的起始或结尾时, n为1

## 参数

- key

    获取元素列表的键

- index

  获取元素在列表中的索引, 从0开始, 可以为负数, 即从列表末尾检索, -1 为倒数第一个元素, -2 为倒数第二个元素, 以此类推

## 返回结果

- Bulk string reply

    指定的元素
    - nil, 指定的索引越界时返回

## 示例

```bash
LINDEX key 8
```