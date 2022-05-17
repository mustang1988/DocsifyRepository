# flattenDeep

---

## 简介

递归将数组的层级深度扁平化到1

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/Libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const data = [1, [2, [3, [4]], 5]];
console.log(_.flattenDeep(data)); // [1, 2, 3, 4, 5]
console.log(data); // [1, [2, [3, [4]], 5]]
```

## 官方文档

[flattenDeep](https://lodash.com/docs/4.17.15#flattenDeep)