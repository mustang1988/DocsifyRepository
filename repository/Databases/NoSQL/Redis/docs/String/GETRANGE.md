# GETRANGE

---

## 官方参考

[GETRANGE官方文档参考](https://redis.io/commands/GETRANGE/)

## 命令语法

> GETRANGE key start end

## 作用

获取指定键对应的值的子字符串

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值的键

- start

  字符串值截取起始索引号, 可以是负数, 表示从字符串末尾向前计算索引号, -1表示倒数第一个字符, -2表示倒数第二个字符, 以此类推, start位置的字符包含在最终结果中

- end

  字符串截取结束索引号, 可以是负数, 表示从字符串末尾向前计算索引号, -1表示倒数第一个字符, -2表示倒数第二个字符, 以此类推, end位置的字符包含在最终结果中

## 返回结果

- Bulk string reply

  截取后的子字符串

## 示例

```bash
GETRANGE key
```