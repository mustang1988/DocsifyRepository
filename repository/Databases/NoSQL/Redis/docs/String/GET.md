# GET

---

## 官方参考

[GET官方文档参考](https://redis.io/commands/GET/)

## 命令语法

> GET key 

## 作用

获取指定键对应的值

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
GET key
```