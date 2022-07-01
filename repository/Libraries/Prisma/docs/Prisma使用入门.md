# Prisma使用入门

---

## 初始化项目

1. 使用NPM初始化项目

    ```bash
    mkdir hello-prisma
    cd hello-prisma
    npm init -y
    npm install prisma typescript ts-node @types/node --save-dev
    ```

2. 项目设置

    在项目目录下新建*tsconfig.json*, 内容如下

    ```json
    {
        "compilerOptions": {
            "sourceMap": true,
            "outDir": "dist",
            "strict": true,
            "lib": ["esnext"],
            "esModuleInterop": true
        }
    }
    ```

3. 初始化Prisma

    ```bash
    npx prisma init
    ```

    初始化完成后, 项目目录下回新增prisma目录, 其中包含文件*schema.prisma*, 初始内容如下

    ```prisma
    // This is your Prisma schema file,
    // learn more about it in the docs: https://pris.ly/d/prisma-schema

    generator client {
        provider = "prisma-client-js"
    }

    datasource db {
        provider = "postgresql"
        url      = env("DATABASE_URL")
    }
    ```

    本文使用的数据库为MySQL, 修改 *datasource db* 下的 *provider* 值为mysql

4. 数据库配置

    在项目目录下新建 *.env* 环境变量配置文件, 至少包含以下内容:

    ```env
    DATABASE_URL="数据库连接地址"
    # 以MySQL 为例:
    # "mysql://<用户名>:<密码>@<IP 地址>:<端口>/<数据库名>"
    ```

    ?> 如果不想使用 *.env* 文件也可以通过修改 *schema.prisma* 中 *datasource db* 下的url, 直接赋值为数据库连接地址

## Schema编写

在 *schema.prisma* 中编写数据库模型的定义如下:

```prisma
model Post {
  id        Int      @id @default(autoincrement())
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  title     String   @db.VarChar(255)
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}

model Profile {
  id     Int     @id @default(autoincrement())
  bio    String?
  user   User    @relation(fields: [userId], references: [id])
  userId Int     @unique
}

model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  name    String?
  posts   Post[]
  profile Profile?
}
```

说明:

- *model*, 用于声明一个数据模型, 其后为模型名称, 模型属性定义在名称后的{}中

- 模型的属性是有类型的, prisma支持以下数据类型
  - 标量类型(Scalar Type)
    - String
    - Boolean
    - Int
    - BigInt
    - Float
    - Decimal
    - DateTime
    - Json
    - Bytes
    - Enum

    标量类型映射到不同数据库实例中默认对应的的类型可参阅: [官方文档](https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference#model-fields)

  - 自定义模型

- 模型的属性修饰符
  - [], 定义属性为列表类型时使用
  - ?, 定义属性为可选, 非必须时使用

- 模型的属性后可以添加注解, 以扩充属性定义, 注解包括以下类型
    - @id(), 定义单属性ID, 该属性不可以为可选属性(修饰符?)
    - @@id(), 定义多属性ID
    - @default(), 定义属性的默认值
    - @unique(), 定义单属性唯一约束
    - @@unique(), 定义多属性唯一约束
    - @@index(), 定义索引
    - @relation(), 定义当前模型与其他模型见的关联关系(数据库外键)
    - @map(), Schema属性名与数据库中字段名不一致时, 用于定义映射关系, Prisma中数据库*字段名*默认情况下是和Schema中定义的*属性名*一致的
    - @@map(), Schema模型名与数据库表名不一致时, 用于定义映射关系, Prisma中数据库*表名*默认情况下是和Schema中定义的*模型*名一致的
    - @updatedAt(), 用于定义数据库值最后更新时间字段, 值由Prisma在更新数据时自信维护
    - @ignore, 用于告知PrismaClient忽略的属性
    - @@ignore, 用于告知PrismaClient忽略的模型

- 模型注解函数, 注解函数是可以用在注解参数中的函数, 包括以下函数
  - auto(), 用于@default()注解, 表示由数据库自动生成默认值
  - autoincrement(), 用于@default()注解, 表示自增默认值
  - sequence(), 用于@default()注解, 表示使用指定序列生成默认值
  - cuid(), 用于@default()注解, 表示使用 *[CUID标准](https://github.com/ericelliott/cuid)* 生成全局唯一标识作为默认值
  - uuid(), 用于@default()注解, 表示使用 *[UUID标准](https://en.wikipedia.org/wiki/Universally_unique_identifier)* 生成全局唯一标识作为默认值
  - now(), 用于@default()注解, 表示使用记录创建时的系统时间戳作为默认值
  - dbgenerated(), 用于@default()注解, 表示不能在Prisma模式中表示的默认值

## 数据库初始化

在项目根目录打开终端执行:

```bash
npx prisma migrate dev --name init
```

执行完成后, 会在prisma目录下创建migrations子目录, 其中存储有建表DDL语句的文件: *migration.sql* 

同时, 数据库中数据表的初始化也已完成

## Prisma基本CRUD的使用

1. 安装prisma客户端

    ```bash
    npm install @prisma/client
    ```

2. 编写CRUD代码

- Create

    ```typescript
    import { PrismaClient } from '@prisma/client'
    const prisma = new PrismaClient()
    // 向User表插入数据
    prisma.user.create({
        data: {
            name: 'Alice',
            email: 'alice@prisma.io',
            posts: {
                create: { title: 'Hello World' },
            },
            profile: {
                create: { bio: 'I like turtles' },
            },
        }
    }).then(new_user => {
        console.log(new_user);
    });
    ```

- Read

    ```typescript
    import { PrismaClient } from '@prisma/client'
    const prisma = new PrismaClient()
    // 查询User表数据
    prisma.user.findMany({
        include: {
            posts: true,
            profile: true,
        },
    }).then(users => {
        console.log(users);
    });
    ```

- Update

    ```typescript
    import { PrismaClient } from '@prisma/client'
    const prisma = new PrismaClient()
    // 更新User表数据
    prisma.post.update({
        where: { id: 1 },
        data: { published: true },
    }).then(result => {
        console.log(result);
    });
    ```

- Delete

    ```typescript
    import { PrismaClient } from '@prisma/client'
    const prisma = new PrismaClient()
    // 删除User表数据
    prisma.post.delete({
        where:{ id: 1 },
    }).then(deleted_record => {
        console.log(deleted_record);
    })
    ```

## 引用

- [Prisma官方文档](https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-typescript-mysql)