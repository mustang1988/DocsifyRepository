# GraphQL Schema定义

---

GraphQL的Schema是有严格数据类型, 数据类型包括标量类型, 枚举类型和自定义类型

## 标量类型

|||
|:-|:-|
|Int|32bit整型|
|Float|浮点数型|
|String|UTF-8字符序列|
|Boolean|true/false|
|ID|一种特殊的String类型, 主要用于数据的唯一标识, GraphQL的缓存机制会基于ID类型字段进行|
|Date|日期类型|

示例

```graphql
type User {
    id: ID
    name: String
    age: Int
    birthday: Date
    score: Float
}
```

## 枚举类型

由开发人员自行定义

示例

```graphql
enum EGender {
  MALE
  FEMALE
}
```

## 自定义类型

完全由开发人员自行定义, 例如上面标量类型示例中的 *User* 就是一个自定义类型, 使用关键字*type*定义

### 接口类型

接口类型是自定义类型的一种, 其定义了一个抽象的类型, 其中包含若干属性, 可被其他自定义类型继承可扩展, 使用关键字*interface*定义

当需要返回一个列表数据, 其中包含了多个不同具体类型的数据时, 将这多个具体类型的数据抽象为接口类型, 就会很有用

示例

```graphql
interface Animal{
    name: String!
}

# Doc类型实现Animal接口, 扩展一个height属性
type Doc implements Animal {
    name: String!
    height: Int!
}

# Cat 类型实现Animal接口, 扩展一个weight属性
type Cat implements Animal {
    name: String!
    weight: Float!
}
```

### 联合类型

联合类型也是自定义类型的一种, 它与接口类型相反, 联合类型允许开发人员联合多个已定义的类型, 成为一个接口类型, 而非从已定义的接口类型向下扩展, 使用关键字*union*定义

示例

```graphql
type Cat {
    name: String!
}
type Dog {
    id: ID!
}

union Animal = Cat | Dog

```

### 输入类型

输入类型是自定义类型的一种, 它的定义方式与一般自定义类型是一样的, 仅仅是使用的关键字不再是*type*, 而是*input*, 输入类型是用于GraphQL进行Query/Mutation操作时输入参数限定类型使用

## 列表类型

列表类型为上述类型的复数类型, 使用*[类型]*标识

示例

```graphql
type User {
    friends: [User]
}
```

## 空/非空限定

GraphQL的Schema定义中可以限定属性的空/非空

对于标量类型和枚举类型, 在类型定义后加*!*即表示该字段为非空限定, 没有*!*即为允许空值

对于列表类i选哪个, 非空限定符*!*既可以在列表类型[]之后也可以在列表[]之中, 分别表示不同的空值限定

- 在[]***后***, 表示该列表类型的属性的值不能为null, 但可以是空列表([]), 其中的元素可以为null
- 在[]***内***, 表示该列表类型的属性的值不能为null, 但可以是空列表([]), 其中的元素也不允许为null

示例

设有如下Schema定义:

```graphql
type User {
    id: ID!
    friends: [User]!
    parents: [User!]
}
```

则空/非空限定的检查结果:

```json
// sample 1
{
    "id": null,                 // invalid
    "friends": [],              // pass
    "parents": []               // pass
}
// sample 2
{
    "id": "1",                  // pass
    "friends": null,            // invalid
    "parents": ["mother", null] // invalid
}
```
