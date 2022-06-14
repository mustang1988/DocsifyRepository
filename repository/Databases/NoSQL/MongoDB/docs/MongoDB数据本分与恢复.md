# MongoDB数据本分与恢复

---

## 数据备份

### 使用mongodump导出数据库

```bash
mongodump --host <host> --port <port> -u <username> -p <password> -d <database> -o <dir>
```

参数说明:

|||
|:-|:-|
|host|数据库地址|
|port|数据库端口|
|username|用户名|
|password|密码|
|database|需要导出的数据库名称|
|dir|导出文件输出目录|

## 数据恢复

### 使用mongorestore导入数据库以恢复

```bash
mongorestore --host <host>:port -u <username> -p <password> <dir>
```

参数说明:

|||
|:-|:-|
|host|数据库地址|
|port|数据库端口|
|username|用户名|
|password|密码|
|dir|mongodump导出的数据目录|