# RPUSH

---

## 官方参考

[RPUSH官方文档参考](https://redis.io/commands/RPUSH/)

## 命令语法

> RPUSH key element [element ...] 

## 作用

向指定键的列表末尾添加元素

如果指定的键不存在, 则会先创建一个空列表, 再进行添加元素操作

## 复杂性

- 时间复杂度

  - O(n), n为添加元素的个数

## 参数

- key

    需要添加元素的列表的键

- element

    需要添加的元素, 可以是多个

## 返回结果

- Integer reply

    添加元素后列表的长度

## 示例

```bash
RPUSH key a b c d
```