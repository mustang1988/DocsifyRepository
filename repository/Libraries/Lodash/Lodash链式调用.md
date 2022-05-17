# Lodash链式调用

---

lodash 支持链式函数调用

## 初始化调用链

### 方式1

```javascript
const _ = require('lodash');
let chain = _(data);
```

### 方式2

```javascript
const _ = require('lodash');
let chain = _.chain(data);
```

## 获取链式调用最终结果

访问调用链的value()函数获取当前调用链的最终结果

```javascript
const _ = require('lodash');
let chain = _(data);
chain.value();  // 获取链式调用最终结果
```

## 复杂链式调用示例

设, 有以下图书数据集

```javascript
const books = [
  { id: 1, name:'Name1-1', category:'社会', archived: false },
  { id: 2, name:'Name1-2', category:'社会', archived: true },
  { id: 3, name:'Name1-3', category:'社会', archived: false },
  { id: 4, name:'Name2-1', category:'自然科学', archived: false },
  { id: 5, name:'Name2-2', category:'自然科学', archived: true },
  { id: 6, name:'Name2-3', category:'自然科学', archived: false },
  { id: 7, name:'Name3-1', category:'计算机', archived: false },
  { id: 8, name:'Name3-2', category:'计算机', archived: true },
  { id: 9, name:'Name3-3', category:'计算机', archived: false },
]
```

现有以下需求:
1. 将上述图书数据按 category 分组
2. 每组中包含2个属性, 组名称(category)和该组的图书列表(books)
3. 其中图书列表只保留 archived 为 false 的数据
4. 每组中的图书按 id 降序排列
5. 每组中的图书信息, 只保留 id 和 name 两个字段

采用链式调用处理上述数据

```javascript
_(books)                                     // 创建链式调用
.groupBy('category')                         // 1. 按 category 分组
.map((books, category) => ({                 // 2. 分组属性转换
	category,
	books: _(books)
        .filter(b => !b.archived)            // 3. 该组图书列表过滤掉 archived 为 true 的值
        .orderBy('id','desc')                // 4. 该组图书列表按 id 降序排序
        .map(b => _.pick(b,['id','name']))   // 5. 该组图书列表只保留 id 和 name 两个属性
        .value();
}))
.value()                                     // 得到最终结果

// 最终返回结果:
// [
//   {
//     category: '社会',
//     books: [
//       { id: 3, name: 'Name1-3' },
//       { id: 1, name: 'Name1-1' }
//     ]
//   },
//   {
//     category: '自然科学',
//     books: [
//       { id: 6, name: 'Name2-3' },
//       { id: 4, name: 'Name2-1' }
//     ]
//   },
//   {
//     category: '计算机',
//     books: [
//       { id: 9, name: 'Name3-3' },
//       { id: 7, name: 'Name3-1' }
//     ]
//   }
// ]
```
