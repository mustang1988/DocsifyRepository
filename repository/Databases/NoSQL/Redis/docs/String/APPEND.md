# APPEND

---

## 官方参考

[APPEND官方文档参考](https://redis.io/commands/APPEND/)

## 命令语法

> APPEND key value

## 作用

向字符串类型值后追加字符串内容

当指定的键不存在时, 会新建该键, 并设置其值为空字符串, 然后对其后追加内容

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要追加内容值的键

- value

  需要追加的字符串内容

## 返回结果

- Integer reply

  追加内容后字符串值的长度

## 示例

```bash
APPEND key "hello"
```