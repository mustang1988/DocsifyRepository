# COPY

---

## 官方参考

[COPY官方文档参考](https://redis.io/commands/COPY/)

## 命令语法

> COPY source destination [DB destination-db] [REPLACE]

## 作用

复制一个键的值到另一个键

## 复杂性

- 时间复杂度

  - 当复制的值为集合类型时, 时间复杂度最差为 O(n), n为被复制集合的大小
  - 当复制字符串值时, 时间复杂度为 O(1)

## 参数

- source

  被复制值的键

- destination

  复制后的键

- DB destination-db

  复制后存储的数据库索引号, 可选, 默认值为当前数据库

- REPLACE

  当目复制后的键已经存在时, 是否先删除已存在的值, 再执行复制, 可选, 默认为不覆盖. 在不覆盖模式下, 当复制后的键已经存在时, 会抛出异常

## 返回结果

- Integer reply

  - 1, 成功复制时返回
  - 0, 复制不成功时返回

## 示例

```bash
COPY old_key new_key
```