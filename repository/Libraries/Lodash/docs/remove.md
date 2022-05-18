# remove

---

## 简介

从数组中移除元素, 同时返回*被移除元素*组成的数组

## 是否影响原引用内容

- 是

## 所属分类

- [Array](/repository/Libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const data = [1, 2, 3, 4];
console.log(_.remove(data, n => {
  return n % 2 == 0;
})); // [2, 4]
console.log(data); // [1, 3]
```

## 官方文档

[remove](https://lodash.com/docs/4.17.15#remove)