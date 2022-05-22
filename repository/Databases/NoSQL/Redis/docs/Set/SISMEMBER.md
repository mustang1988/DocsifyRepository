# SISMEMBER

---

## 官方参考

[SISMEMBER官方文档参考](https://redis.io/commands/SISMEMBER/)

## 命令语法

> SISMEMBER key member

## 作用

检查指定元素是否是指定键对应set的成员

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要检索的set的键

- member

  需要检查的元素

## 返回结果

- Integer reply

  - 1, 指定的元素是指定键对应set的成员时返回
  - 0, 指定的元素*不是*指定键对应set的成员, 获指定的键不存在时返回

## 示例

```bash
SISMEMBER key "hello"
```