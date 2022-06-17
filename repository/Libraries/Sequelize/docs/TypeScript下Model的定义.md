# TypeScript下Model的定义

---

## 安装依赖

```bash
npm install sequelize reflect-metadata sequelize-typescript
```

## 配置tsconfig

在tsconfig.json配置文件的"compilerOptions"属性下添加配置, 启用Decorator

```json
"experimentalDecorators": true,
"emitDecoratorMetadata":true,
"strictPropertyInitialization": false
```

## 编写Model类

示例: 

```typescript
import {
    Column,
    CreatedAt,
    DataType,
    Model,
    UpdatedAt,
} from 'sequelize-typescript';

@Table({
    tableName: 'tb_node',
    timestamps: true,
    charset: 'utf8mb4',
    collate: 'utf8mb4_general_ci',
})
export class Job extends Model {
    @Column({
        type: DataType.TEXT,
        primaryKey: true,
        unique: true,
    })
    id: string;

    @Column({
        type: DataType.TEXT,
    })
    job_task_id: string;

    @Column({
        type: DataType.TEXT,
    })
    job_node_id: string;

    @Column({
        type: DataType.TEXT,
    })
    job_status: string;

    @Column({
        type: DataType.NUMBER,
    })
    job_retried: number;

    @Column({
        type: DataType.TEXT,
    })
    job_file: string;

    @Column({
        type: DataType.TEXT,
    })
    job_args: string;

    @Column({
        type: DataType.TEXT,
    })
    job_log: string;

    @CreatedAt
    created_at: Date;

    @UpdatedAt
    updated_at: Date;
}
```

相关注解:

||||
|:-|:-|:-|
|@Table|声明映射的数据库表||
|@Column|声明映射的数据库字段||
|@CreatedAt|声明映射到记录创建时间属性||
|@UpdatedAt|声明映射到记录更新时间属性||