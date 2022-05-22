# RPUSHX

---

## 官方参考

[RPUSHX官方文档参考](https://redis.io/commands/RPUSHX/)

## 命令语法

> RPUSHX key element [element ...]

## 作用

最用与[RPUSH](/repository/Databases/NoSQL/Redis/docs/List/RPUSH.md)几乎一样, 仅有一点不同

当指定的键不存在时, RPUSHX 不会创建一个空列表再把元素放入, 而是什么都不做

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
RPUSHX key a b c d
```