# EXISTS

---

## 官方参考

[EXISTS官方文档参考](https://redis.io/commands/EXISTS/)

## 命令语法

> EXISTS key [key...]

## 作用

返回指定的键是否存在

## 复杂性

- 时间复杂度

  - O(n), n为指定的键的数量

## 参数

- key

  被检查的键

## 返回结果

- Integer reply

  指定键中存在的数量

  !> 注意, 当指定参数中存在重复的键, 返回结果的数量并不会将重复的键做过滤处理<br/>
  例如:<br/>
  EXISTS key key<br/>
  如果key存在, 则返回结果是2, 并不是1.

## 示例

```bash
# 检查单个键
EXISTS key
# 检查多个键
EXISTS key1 key2 key3
```