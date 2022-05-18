# meanBy

---

## 简介

附过滤条件的数组元素平均值计算

## 是否影响原引用内容

- 否

## 参数说明

```javascript
_.meanBy(array, [iteratee=_.identity])
```

- array

  需要计算平均值的数组

- iteratee

  过滤选择条件函数, 可选

## 所属分类

- [Math相关函数](/repository/Libraries/Lodash/Math.md#math相关函数)

## 示例

```javascript
const _ = require('lodash');
const objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];
_.meanBy(objects, function(o) { return o.n; }); // 5
_.meanBy(objects, 'n'); // 5
```

## 官方文档

[meanBy](https://lodash.com/docs/4.17.15#meanBy)