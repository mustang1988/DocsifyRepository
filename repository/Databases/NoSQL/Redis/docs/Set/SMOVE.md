# SMOVE

---

## 官方参考

[SMOVE官方文档参考](https://redis.io/commands/SMOVE/)

## 命令语法

> SMOVE source destination member 

## 作用

将指定成员从一个set移动到另一个set, 这是一个原子操作

当源set不存在或不包含指定元素时, 不会进行任何操作, 反正, 指定元素将被从源set中移除, 同时加入到目标set中, 如果目标set中已经包含该元素, 则仅将源set中的指定元素移除

如果指定的源键获目标键对应数据不是set, 则抛出异常

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- source

  源set的键

- destination

  目标set的键

- member

  需要进行移动的元素

## 返回结果

- Integer reply

  - 1, 元素移成功时返回
  - 0, 指定元素不在源set中, 无事发生时返回

## 示例

```bash
# 将key1集合中的"hello"移动到key2集合中
SMOVE key key2 "hello"
```