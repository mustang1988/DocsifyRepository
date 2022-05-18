# 存储Object类型数据时设置默认值{}无效的问题

---

## 现象

在Mongoose的模型类中定义了某Object类型字段的 default 为 {}

当插入新数据不指定该字段并入库后, 检查数据库中该新增数据的该字段的值, 发现该字段值并未填充为 {}, 而是 undefined

## 解决方案

Mongoose模型定义的option参数中设置minimize为false, 默认值为true

## 示例

```javascript
// TODO
```