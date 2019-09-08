title: Node之Express框架
typora-root-url: ..
tags:
  - Express
  - ''
categories:
  - Node
date: 2019-09-06 12:22:00
password:
top:
---

###  先安装

```
npm install express --save
```

### 创建一个hello world

```javascript
var express = require('express')

var app = express()

app.get('/',function(req,res){
  res.send('hello world')
})

app.listen(4000,function(){
  console.log('star 4000')
})
```

###  express 静态服务 API

```javascript
app.use('/public/', express.static('./public'))

//另一种用法 路径省略public
app.use(express.static('./public'))

//标识  访问的时候路径中用a来替换public 
app.use('/a/', express.static('./public'))
```

### 修改完代码自动重启

```shell
npm install --global nodemon
```

使用方法

```shell
node app.js

#替换为
nodemon app.js
```

### 基本路由

> get:
>
> ```javascript
> app.get('/',function(req,res){
>   res.send('hello world')
> })
> ```
>
> post:
>
> ```javascript
> app.post('/',function(req,res){
>   res.send('hello world')
> })
> ```

---



### 在`Express`中配置使用 `art-template` 模板引擎

> [官方文档](https://aui.github.io/art-template/)
>
> [仓库](https://github.com/aui/art-template)

安装：

```shell
npm install --save art-template
npm install --save express-art-template
```

配置：

```javascript
app.engine('html', require('express-art-template'))
```
使用：
```javascript
app.get('/',function(req,res){
  res.render('index.html',{
      title: 'aaa'
  })
})
```

默认约定界面文件在 views 目录

如果想要修改默认的 views 目录，则可以

```javascript
app.set('views', 要设置的默认路径)
```

### 重定向

```javascript
// res.statusCode = 302
// res.setHeader('Location', '/') 
//原来需要这样
res.redirect('/')
```





---

### 表单GET

req.query 只能拿 get 请求参数

### 表单POST

拿post请求体没有内置API，需要第三方包： 、

### **body-parser**

```sh
npm install body-parser --save
```

配置：

```javascript
var express = require('express')
//1.导包
var bodyParser = require('body-parser')

var app = express()

//配置 body-parser
//只要加入这个配置，在req请求对象上会多出来一个属性：body
//通过req.body来获取数据


// 配置 body-parser 中间件（插件，专门用来解析表单 POST 请求体）
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))

// parse application/json
app.use(bodyParser.json())




app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
```

