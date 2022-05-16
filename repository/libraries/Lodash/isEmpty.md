# isEmpty

---

## 简介

判断指定变量的值是否是"空"的

"空"的定义为：
- 长度为0的Array, Set, Map
- null
- undefinde
- 任意数值或没有自己的可枚举字符串键属性
- ""
- {}

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- [Lang相关函数](/repository/libraries/Lodash/Lang.md#lang相关函数)

## 示例

```javascript
const _ = require('lodash');
_.isEmpty(null); // true
_.isEmpty(true); // true
_.isEmpty(1); // true
_.isEmpty([1, 2, 3]); // false
_.isEmpty({ a: 1 }); // false
```

## 官方文档

[isEmpty](https://lodash.com/docs/4.17.15#isEmpty)