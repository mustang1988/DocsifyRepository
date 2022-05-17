# clamp

---

## 简介

在限定上下限范围内取值

如果给定的数值不在上下限的范围内
- 如果小于下限值则返回下限值
- 如果大于上限值则返回上限值

如果给定的值在上下限的范围内, 则返回该给定的值


## 是否影响原引用内容

- 否

## 参数说明

```javascript
_.clamp(number, [lower], upper)
```

- number

    给定的数值

- lower

    取值下限, 可选
    
- upper
        
    取值上限

## 所属分类

- [Math相关函数](/repository/Libraries/Lodash/Math.md#math相关函数)

## 示例

```javascript
const _ = require('lodash');
_.clamp(1.5, 1, 2) // 1.5, 给定值1.5在[1,2]区间内
_.clamp(-1, 1, 2)  // 1, 给定值-1小于[1,2]区间
_.clamp(3, 1, 2)   // 2, 给定值3大于[1,2]区间
```

## 官方文档

[clamp](https://lodash.com/docs/4.17.15#clamp)