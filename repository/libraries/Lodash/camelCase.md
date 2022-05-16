# camelCase

---

## 简介

将字符串转换为*小*驼峰格式

## 是否影响原引用内容

- 否

## 参数说明

- 

## 所属分类

- 

## 示例

```javascript
const _ = require('lodash');
_.camelCase('Foo Bar'); // 'fooBar'
_.camelCase('--foo-bar--'); // 'fooBar'
_.camelCase('__FOO_BAR__'); // 'fooBar'
```

## 官方文档

[camelCase](https://lodash.com/docs/4.17.15#camelCase)