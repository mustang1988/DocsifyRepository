# compact

---

## 简介

去除数组中的"空值"

"空值"包括
- false
- null
- 0
- ""
- undefined
- NaN 

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const data = [0, 1, '2', '', null, undefined, {}, false, true, NaN];
console.log(_.compact(data)); // [ 1, '2', {}, true ]
console.log(data); // [ 0, 1, '2', '', null, undefined, {}, false, true, NaN ]
```

## 官方文档

[compact](https://lodash.com/docs/4.17.15#compact)