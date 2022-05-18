# groupBy

---

## 简介

对数组/集合进行分组

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- [Array](/repository/Libraries/Lodash/Array.md#array相关函数)
- [Collection](/repository/Libraries/Lodash/Collection.md#collection相关函数)

## 示例

```javascript
const _ = require('lodash');
_.groupBy([6.1, 4.2, 6.3], Math.floor); // { '4': [4.2], '6': [6.1, 6.3] }
_.groupBy(['one', 'two', 'three'], 'length'); // { '3': ['one', 'two'], '5': ['three'] }
```

## 官方文档

[groupBy](https://lodash.com/docs/4.17.15#groupBy)