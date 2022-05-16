# map

---

## 简介

对给定数组/集合进行遍历, 对每个元素执行同一函数, 返回执行函数后形成的新数组/集合

## 是否影响原引用内容

- 否

## 参数说明

- 否

## 所属分类

- [Array](/repository/libraries/Lodash/Array.md#array相关函数)
- [Collection](/repository/libraries/Lodash/Collection.md#collection相关函数)

## 示例

```javascript
const _ = require('lodash');
function square(n) {
  return n * n;
}
_.map([4, 8], square); // [16, 64]
_.map({ 'a': 4, 'b': 8 }, square); // [16, 64]
const users = [
  { 'name': 'barney' },
  { 'name': 'fred' }
];
_.map(users, 'name');// ['barney', 'fred']
```

## 官方文档

[map](https://lodash.com/docs/4.17.15#map)