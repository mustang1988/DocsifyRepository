# SCARD

---

## 官方参考

[SCARD官方文档参考](https://redis.io/commands/SCARD/)

## 命令语法

> SCARD key 

## 作用

获取指定键对应set的长度

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

  需要获取长度的键

## 返回结果

- Integer reply

  指定键对应set的长度
  - 0, 当指定的键不存在时返还

## 示例

```bash
SCARD key
```