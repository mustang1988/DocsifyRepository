# HLEN

---

## 官方参考

[HLEN官方文档参考](https://redis.io/commands/HLEN/)

## 命令语法

> HLEN key 

## 作用

获取指定键对应hash的长度

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取hash长度的键

## 返回结果

- Integer reply

  指定hash长度
  - 0, 指定键不存在时返回

## 示例

```bash
HLEN key
```