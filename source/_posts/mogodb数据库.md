title: MogoDB数据库
typora-root-url: ..
tags:
  - MongoDB
categories:
  - Node
date: 2019-09-07 17:50:00
password:
top:
---
# 配置MongoDB

1. 配置环境变量：

   **path添加 安装目录下/bin**

```
C:\Develop\mongodb\bin
```

> 已经在 C 盘安装了 mongodb，现在让我们创建一个 data 的目录然后在 data 目录里创建 db 目录。
>
> C:\data\db

2. 开启：

```shell
mongod
```

3. 连接数据库：(再开一个cmd)

```shell
#连接本机的MongoDB数据库
mongo
#退出
exit
```

4. 基本命令：

```shell
#查看显示所有数据库
show dbs
#查看当前的数据库
db
#切换到指定的数据库（如果没有会新建）
use 数据库名称
#插入数据(新建表名students插入数据)
db.students.insertOne("name":"jack")
#查看数据
show collections
db.students.find()
```

### 在node中如何操作MongoDB数据

使用官方的mongodb的包

[github包](https://github.com/mongodb/node-mongodb-native)

基于MongoDB官方的包再一次做了封装mongoose

[mongoose](https://mongoosejs.com/)