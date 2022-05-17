# get

---

## 简介

获取对象指定属性的值，可以指定多级属性，如果属性不存在，返回 undefined

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- 

## 示例

```javascript
const _ = require('lodash');
var object = { 'a': [{ 'b': { 'c': 3 } }] };
_.get(object, 'a[0].b.c'); // 3
_.get(object, ['a', '0', 'b', 'c']); // 3
_.get(object, 'a.b.c', 'default'); // 'default'
```

## 官方文档

[get](https://lodash.com/docs/4.17.15#get)