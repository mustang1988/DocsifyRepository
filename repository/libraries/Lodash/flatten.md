# flatten

---

## 简介

将数组的层级深度扁平化一个层级

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const data = [1, [2, [3, [4]], 5]];
console.log(_.flatten(data)); // [ 1, 2, [ 3, [ 4 ] ], 5 ]
console.log(data); // [1, [2, [3, [4]], 5]]
```

## 官方文档

[flatten](https://lodash.com/docs/4.17.15#flatten)