# intersectionBy

---

## 简介

对多个数组数据附条件取交集

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/Libraries/Lodash/Array.md#array相关函数)
- [Collection](/repository/Libraries/Lodash/Collection.md#collection相关函数)

## 示例

```javascript
const _ = require('lodash');
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor); // => [2.1]
_.intersectionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x'); // => [{ 'x': 1 }]
```

## 官方文档

[intersectionBy](https://lodash.com/docs/4.17.15#intersectionBy)