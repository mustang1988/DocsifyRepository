# isNil

---

## 简介

判断指定变量的值是否是*null*或*undefined*

## 是否影响原引用内容

- 否

## 所属分类

- [Lang](/repository/libraries/Lodash/Lang.md#lang相关函数)

## 示例

```javascript
const _ = require('lodash');
console.log(_.isNil({})); // false
console.log(_.isNil(1)); // false
console.log(_.isNil(null)); // true
console.log(_.isNil(undefined)); // true
```

## 官方文档

[isNil](https://lodash.com/docs/4.17.15#isNil)