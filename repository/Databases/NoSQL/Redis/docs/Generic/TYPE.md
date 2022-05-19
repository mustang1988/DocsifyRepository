# TYPE

---

## 官方参考

[TYPE官方文档参考](https://redis.io/commands/TYPE/)

## 命令语法

> TYPE key 

## 作用

获取指定键对应值的类型

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取值类型的键

## 返回结果

- Simple string reply
  
  键所对应值的类型
  - string
  - list
  - set
  - zset
  - hash
  - stream
  - none, 当指定的键不存在时返回

## 示例

```bash
TYPE key
```