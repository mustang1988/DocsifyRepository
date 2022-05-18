# random

---

## 简介

生成指定上下限范围内的随机数

## 是否影响原引用内容

- 否

## 参数说明

```javascript
_.random([lower=0], [upper=1], [floating])
```

- lower

    下限, 可选, 默认值: 0

- upper

    上限, 可选, 默认值: 1

- floating

    是否返回浮点数, 可选, 默认值, 根据上下限值的类型决定


## 所属分类

- [Math相关函数](/repository/Libraries/Lodash/Math.md#math相关函数)

## 示例

```javascript
const _ = require('lodash');
_.random(0, 5); // => an integer between 0 and 5
_.random(5); // => also an integer between 0 and 5
_.random(5, true); // => a floating-point number between 0 and 5
_.random(1.2, 5.2); // => a floating-point number between 1.2 and 5.2
```

## 官方文档

[random](https://lodash.com/docs/4.17.15#random)