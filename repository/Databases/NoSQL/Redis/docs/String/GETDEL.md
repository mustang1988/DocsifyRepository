# GETDEL

---

## 官方参考

[GETDEL官方文档参考](https://redis.io/commands/GETDEL/)

## 命令语法

> GETDEL key 

## 作用

与[GET](/repository/Databases/NoSQL/Redis/docs/String/GET.md)类似, 获取指定键对应的值, 但在成功获取值后会删除对应的键, 当且仅当值类型为字符串.

如果指定的键对应的值不是字符串格式的, 则抛出异常

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值的键

## 返回结果

- Bulk string reply
  
  键对应的字符串值

  - nil, 当指定的键不存在时返回

## 示例

```bash
GETDEL key
```