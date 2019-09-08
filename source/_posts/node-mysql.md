title: Node+mysql
typora-root-url: ..
tags:
  - node-mysql
categories:
  - Node
date: 2019-09-08 15:02:00
password:
top:
---

# 使用Node操作MySQL数据库


安装：

```shell
npm install mysql
```

```javascript
var mysql = require('mysql');

// 1. 创建连接
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '123456',
  database: 'users'
});

// 2. 连接数据库 打开冰箱门
connection.connect();

// 3. 执行数据操作 把大象放到冰箱
connection.query('SELECT * FROM `users`', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});

// connection.query('INSERT INTO users VALUES(NULL, "admin", "123456")', function (error, results, fields) {
//   if (error) throw error;
//   console.log('The solution is: ', results);
// });

// 4. 关闭连接 关闭冰箱门
connection.end();
```