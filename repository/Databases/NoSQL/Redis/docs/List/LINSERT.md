# LINSERT

---

## 官方参考

[LINSERT官方文档参考](https://redis.io/commands/LINSERT/)

## 命令语法

> LINSERT key BEFORE | AFTER pivot element 

## 作用

向指定键列表的指元素的前/后面插入元素

## 复杂性

- 时间复杂度

  - O(n), n为找到指定的元素需要经历的次数, 当指定的元素位于列表的起始或结尾时, n为1

## 参数

- key

    需要插入元素的列表的键

- BEFORE | AFTER

    在指定元素前/后方插入新元素

- pivot

    检索的元素

- element

    插入的元素

## 返回结果

- Integer reply

    返回插入元素后列表的长度
    - -1, 当指元素在列表中未找到时返回

## 示例

```bash
# 在key对应的列表中"hello"元素之后插入"world"元素
LINSERT key AFTER "hello" "world"
```