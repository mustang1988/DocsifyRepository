# omit

---

## 简介

[pick](/repository/Libraries/Lodash/pick.md#pick) 的反向操作, 忽略对象中的指定属性, 返回其他属性构成的对象

## 是否影响原引用内容

- 否

## 参数说明

```javascript
_.omit(object, [paths])
```

- object

    需要操作的对象

- paths

    需要忽略的属性路径/需要忽略的属性路径数组

## 所属分类

- [Object相关函数](/repository/Libraries/Lodash/Object.md#object相关函数)

## 示例

```javascript
const _ = require('lodash');
var object = { 'a': 1, 'b': '2', 'c': 3 };
_.omit(object, ['a', 'c']); // { 'b': '2' }
_.omit({name:'hello', age:20, sex:'male', others:{ id:'1', value:2 } },['name', 'others.id']); // { age: 20, sex: 'male', others: { value: 2 } }
```

## 官方文档

[omit](https://lodash.com/docs/4.17.15#omit)