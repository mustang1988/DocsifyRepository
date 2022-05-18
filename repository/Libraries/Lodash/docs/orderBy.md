# orderBy

---

## 简介

对数组/集合进行排序

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- [Array](/repository/Libraries/Lodash/Array.md)
- [Collection](/repository/Libraries/Lodash/Collection.md#collection相关函数)

## 示例

```javascript
const _ = require('lodash');
var users = [
  { user: 'fred', age: 48 },
  { user: 'barney', age: 34 },
  { user: 'fred', age: 40 },
  { user: 'barney', age: 36 },
];
console.log(_.orderBy(users, ['user', 'age'], ['asc', 'desc']));
/**
 * [
  { user: 'barney', age: 36 },
  { user: 'barney', age: 34 },
  { user: 'fred', age: 48 },
  { user: 'fred', age: 40 }
   ]
*/
console.log(users);
/**
 * [
   { user: 'fred', age: 48 },
   { user: 'barney', age: 34 },
   { user: 'fred', age: 40 },
   { user: 'barney', age: 36 }
   ]
*/
```

## 官方文档

[orderBy](https://lodash.com/docs/4.17.15#orderBy)