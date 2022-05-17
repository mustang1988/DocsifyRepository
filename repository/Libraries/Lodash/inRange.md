# inRange

---

## 简介

检查指定值是否在上下限范围内

## 是否影响原引用内容

- 否

## 参数说明

```javascript
_.inRange(number, [start=0], end)
```

- number

    需要检查的数值

- start

    下限, 可选, 默认值: 0

- end

    上限

## 所属分类

- [Math相关函数](/repository/Libraries/Lodash/Math.md#math相关函数)

## 示例

```javascript
const _ = require('lodash');
_.inRange(3, 2, 4); // true 
_.inRange(4, 8); // true 
_.inRange(4, 2); // false 
_.inRange(2, 2); // false
_.inRange(1.2, 2); // true
_.inRange(5.2, 4); // false
_.inRange(-3, -2, -6); // true
```

## 官方文档

[inRange](https://lodash.com/docs/4.17.15#inRange)