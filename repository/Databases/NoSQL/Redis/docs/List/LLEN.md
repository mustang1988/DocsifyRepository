# LLEN

---

## 官方参考

[LLEN官方文档参考](https://redis.io/commands/LLEN/)

## 命令语法

> LLEN key 

## 作用

获取指定键对应列表的长度

如果指定的键对应的值不是列表类型, 抛出异常

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

    需要获取长度的列表的键

## 返回结果

- Integer reply

    列表的长度

## 示例

```bash
LLEN key
```