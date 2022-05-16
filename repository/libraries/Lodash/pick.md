# pick

---

## 简介

获取对象中指定部分属性的内容

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- 

## 示例

```javascript
const _ = require('lodash');
var object = { 'a': 1, 'b': '2', 'c': 3 };
_.pick(object, ['a', 'c']); // { 'a': 1, 'c': 3 }
```

## 官方文档

[pick](https://lodash.com/docs/4.17.15#pick)