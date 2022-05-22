# SADD

---

## 官方参考

[SADD官方文档参考](https://redis.io/commands/SADD/)

## 命令语法

> SADD key member [member ...]

## 作用

将指定的一个或多个成员加入到指定键的set中, 如果指定的成员已经在set中, 则会被忽略, 如果指定的键不存在, 会先创建该键后再存入成员

如果指定的键对应的值不是set类型, 抛出异常

## 复杂性

- 时间复杂度

  - O(n), n为实际加入set的成员数量

## 参数

- key

  需要添加成员的键

- member

  需要加入set的成员, 可以是多个

## 返回结果

- Integer reply

  成功加入的成员数量

## 示例

```bash
SADD key a b c
```