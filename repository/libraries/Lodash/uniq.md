# uniq

---

## 简介

数组去重

## 是否影响原引用内容

- 否

## 所属分类

- [Array](/repository/libraries/Lodash/Array.md#array相关函数)

## 示例

```javascript
const _ = require('lodash');
const data = [1,2,1];
console.log(_.uniq(data)); // [1,2]
console.log(data); // [1,2,1]
```

## 官方文档

[uniq](https://lodash.com/docs/4.17.15#uniq)