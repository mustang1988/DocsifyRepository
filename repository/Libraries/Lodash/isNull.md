# isNull

---

## 简介

判断指定变量的值是否为*null*

## 是否影响原引用内容

- 否

## 所属分类

- [Lang](/repository/Libraries/Lodash/Lang.md#lang相关函数)

## 示例

```javascript
const _ = require('lodash');
console.log(_.isNull({})); // false
console.log(_.isNull(1)); // false
console.log(_.isNull(null)); // true
console.log(_.isNull(undefined)); // false
```

## 官方文档

[isNull](https://lodash.com/docs/4.17.15#isNull)