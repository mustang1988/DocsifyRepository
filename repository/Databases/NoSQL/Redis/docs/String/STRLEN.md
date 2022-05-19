# STRLEN

---

## 官方参考

[STRLEN官方文档参考](https://redis.io/commands/STRLEN/)

## 命令语法

> STRLEN key 

## 作用

获取指定键对应字符串值的长度

## 复杂性

- 时间复杂度

  - O(1)

## 参数

- key

    需要获取值长度的键

## 返回结果

- Integer reply

    字符串值的长度

    - 0, 键不存在时返回

## 示例

```bash
STRLEN key
```