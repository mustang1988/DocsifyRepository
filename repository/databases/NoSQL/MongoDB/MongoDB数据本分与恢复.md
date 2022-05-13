# MongoDB数据本分与恢复

---

## 数据备份

### 使用mongodump导出数据库

```shell
mongodump --host 数据库地址 --port 数据库端口 -u 用户名 -p 密码 -d 需要导出的数据库名称 -o 导出文件输出目录
```

## 数据恢复

### 使用mongorestore导入数据库以恢复

```shell
mongorestore --host 数据库地址:数据库端口 -u 用户名 -p 密码 mongodump导出的数据目录
```