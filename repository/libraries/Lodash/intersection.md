# intersection

---

## 简介

对多个数组的数据取交集

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const arr_1 = [1,2,3];
const arr_2 = [2,3,4];
const arr_3 = [3,4,5];
console.log(_.intersection(arr_1, arr_2)); // [2,3]
console.log(_.intersection(arr_2, arr_3)); // [3,4]
console.log(_.intersection(arr_1, arr_2, arr_3)); // [3]
```

## 官方文档

[intersection](https://lodash.com/docs/4.17.15#intersection)