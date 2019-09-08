title: Node+express+MongoDB的crud案例
typora-root-url: ..
tags:
  - MongoDB
  - ''
  - Node
  - Express
categories:
  - Node
date: 2019-09-08 15:02:00
password:
top:
---

# 基于express的crud

## 总结

1. 安装

   ```shell
   #使用express搭建服务器
   npm install express
   #模板引擎页面渲染 定向
   npm install express-art-template art-template
   #用来处理POST请求 获取请求体(req.body)
   npm install body-parser
   #提供MongoDB的crud
   npm install mongoose
   ```

2. express要点

   > - 设置 静态服务（url可访问）
   >
   > - 把路由容器挂载到 app 服务中
   >   app.use(router)
   >
   > - Express 提供了一种更好的方式 专门用来包装路由的
   >   var express = require('express')
   >
   >   创建一个路由容器
   >   var router = express.Router()
   >
   >   执行
   >
   >   router.get()
   >
   >   router.post()

3. 表单要点

   > get  ===> req.query 拿 get 请求参数
   > post ===> req.body 拿post请求参数

4. mongoose要点

   > 注意格式
   > id 是字符串格式且 为 ( _id )
   > 记得去字符串

5. art-template要点

   > 模板配置（默认约定文件在views目录）
   > app.engine('html', require('express-art-template'))

   > 渲染页面
   >
   > ```
   > router.get('/students', function (req, res) {
   > 
   > 	res.render('new.html')
   > 
   > }
   > ```
   >
   > 重定向
>
   > ```
   > res.redirect('/students')
   > ```
   
   > 循环语法
   >
   > ```
   > {{ each students }} 
   > 
   > {{ $value.hobbies }}
   > 
   > {{ /each }}
   > ```

## 路由设计

| 请求方法 | 请求路径         | get 参数 | post 参数                      | 备注             |
| -------- | ---------------- | -------- | ------------------------------ | ---------------- |
| GET      | /studens         |          |                                | 渲染首页         |
| GET      | /students/new    |          |                                | 渲染添加学生页面 |
| POST     | /studens/new     |          | name、age、gender、hobbies     | 处理添加学生请求 |
| GET      | /students/edit   | id       |                                | 渲染编辑页面     |
| POST     | /studens/edit    |          | id、name、age、gender、hobbies | 处理编辑请求     |
| GET      | /students/delete | id       |                                | 处理删除请求     |
|          |                  |          |                                |                  |

### 入口模块（app.js）

```javascript
/**
 * app.js 入口模块
 * 职责：
 *   创建服务
 *   做一些服务相关配置
 *     模板引擎
 *     body-parser 解析表单 post 请求体
 *     提供静态资源服务
 *   挂载路由
 *   监听端口启动服务
 */
var express = require('express')

//用来处理post表单请求体（req.body）
var bodyParser = require('body-parser')

var router = require('./router')

var app = express()

//设置 静态服务（url可访问）
app.use('/node_modules/', express.static('./node_modules/'))
app.use('/public/', express.static('./public/'))

//模板配置（默认约定文件在views目录）：
app.engine('html', require('express-art-template'))

// 配置模板引擎和 body-parser 一定要在 app.use(router) 挂载路由之前
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())



// router(app)

// 把路由容器挂载到 app 服务中
app.use(router)


app.listen(4000, function () {
  console.log('running 4000...')
})

module.exports = app

```

### 数据操作文件模块（student.js）

```javascript
/**
 * student.js 操作数据模块
 * 职责：操作文件中的数据，只处理数据，不关心业务
 */

var mongoose = require('mongoose')

var Schema = mongoose.Schema

//连接数据库
mongoose.connect('mongodb://localhost/itcast')

//定义表单 设计文档结构
var studentSchema = new Schema({
  name : {
    type: String,
    required: true //必填
  },
  gender: {
    type: Number,
    enum: [0, 1], //0或者1
    default: 0
  },
  age: {
    type: Number //可为空
  },
  hobbies : {
    type: String //可为空
  }
})

// 发布为模型 并导出给router模块执行crud（注意生成的集合为小写复数students）
// 模型构造函数
module.exports = mongoose.model('Student',studentSchema)
```

### 路由模块（router.js）

```javascript
/**
 * router.js 路由模块
 * 职责：
 *   处理路由
 *   根据不同的请求方法+请求路径设置具体的请求处理函数
 * 模块职责要单一，不要乱写
 * 划分模块的目的就是为了增强项目代码的可维护性
 * 提升开发效率
 */

var fs = require('fs')

// 接收模型构造函数 用来执行crud
var Student = require('./student')

// Express 提供了一种更好的方式
// 专门用来包装路由的
var express = require('express')

// 1. 创建一个路由容器
var router = express.Router()

// 2. 把路由都挂载到 router 路由容器中

/*
 * 渲染学生列表页面
 */
router.get('/students', function (req, res) {

    Student.find(function(err, students){
      if(err){
        return res.status(500).send('sever error')
      }
      res.render('index.html', {
        fruits: [
          '苹果',
          '香蕉',
          '橘子'
        ],
        students: students
      })
    })
    
})

/*
 * 渲染添加学生页面
 */
router.get('/students/new', function (req, res) {
  res.render('new.html')
})

/*
 * 处理添加学生
 */
router.post('/students/new', function (req, res) {
  // 1. 获取表单数据
  // 2. 处理
  // 3. 发送响应
  new Student(req.body).save(function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/students')
  })
})

/*
 * 渲染编辑学生页面
 */
router.get('/students/edit', function (req, res) {
  // 1. 在客户端的列表页中处理链接问题（需要有 id 参数）
  // 2. 获取要编辑的学生 id 
  // 3. 渲染编辑页面
  //    根据 id 把学生信息查出来
  //    使用模板引擎渲染页面
  
  //MongoDB的id是字符串格式的需处理一下且对应html文件中需要注意id是带带下划线的(_id)

  Student.findById(req.query.id.replace(/"/g, ''), function (err, student) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.render('edit.html', {
      student: student
    })
  })
})

/*
 * 处理编辑学生
 */
router.post('/students/edit', function (req, res) {
  // 1. 获取表单数据
    //  req.body
    //  console.log(req.body)
  // 2. 更新
    //  Student.updateById()
  // 3. 发送响应
  var id = req.body.id.replace(/"/g, '')
  Student.findByIdAndUpdate(id, req.body, function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/students')
  })
})

/*
 * 处理删除学生
 */
router.get('/students/delete', function (req, res) {
  // 1. 获取要删除的 id
  // 2. 根据 id 执行删除操作
  // 3. 根据操作结果发送响应数据
  var id = req.query.id.replace(/"/g, '')
  Student.findByIdAndRemove(id, function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/students')
  })
})

// 3. 把 router 导出
module.exports = router

```

### views的文件

#### new.html

1. 这里会自动生成id
2. 故只需要  name、age、gender、hobbies

```html
<div class="col-sm-9 col-sm-offset-3 col-md-10 col-md-offset-2 main">
        <h2 class="sub-header">添加学生</h2>
        <form action="/students/new" method="post">
          <div class="form-group">
            <label for="">姓名</label>
            <input type="text" class="form-control" id="" name="name" required minlength="2" maxlength="10">
          </div>
          <div class="form-group">
            <label for="">性别</label>
            <div>
              <label class="radio-inline">
                <input type="radio" name="gender" id="" value="0" checked> 男
              </label>
              <label class="radio-inline">
                <input type="radio" name="gender" id="" value="1"> 女
              </label>
            </div>
          </div>
          <div class="form-group">
            <label for="">年龄</label>
            <input class="form-control" type="number" id="" name="age" required min="1" max="150">
          </div>
          <div class="form-group">
            <label for="">爱好</label>
            <input class="form-control" type="text" id="" name="hobbies">
          </div>
          <button type="submit" class="btn btn-default">Submit</button>
        </form>
      </div>
```

### edit.html

1. 注意id在mongodb中是 （ _id )
2. 修改需要提交  id、name、age、gender、hobbies

```html
<div class="col-sm-9 col-sm-offset-3 col-md-10 col-md-offset-2 main">
        <h2 class="sub-header">添加学生</h2>
        <form action="/students/edit" method="post">
          
          <!-- 
            用来放一些不希望被用户看见，但是需要被提交到服务端的数据
           -->
          <input type="hidden" name="id" value="{{ student._id }}">

          <div class="form-group">
            <label for="">姓名</label>
            <input type="text" class="form-control" id="" name="name" required minlength="2" maxlength="10" value="{{ student.name }}">
          </div>
          <div class="form-group">
            <label for="">性别</label>
            <div>
              <label class="radio-inline">
                <input type="radio" name="gender" id="" value="0" checked> 男
              </label>
              <label class="radio-inline">
                <input type="radio" name="gender" id="" value="1"> 女
              </label>
            </div>
          </div>
          <div class="form-group">
            <label for="">年龄</label>
            <input class="form-control" type="number" id="" name="age" value="{{ student.age }}" required min="1" max="150">
          </div>
          <div class="form-group">
            <label for="">爱好</label>
            <input class="form-control" type="text" id="" name="hobbies" value="{{ student.hobbies }}">
          </div>
          <button type="submit" class="btn btn-default">Submit</button>
        </form>
      </div>
```

#### index.html

1. 模板循环语法each

```html
 <table class="table table-striped">
              <thead>
                <tr>
                    <th>#</th>
                    <th>姓名</th>
                    <th>性别</th>
                    <th>年龄</th>
                    <th>爱好</th>
                    <th>操作</th>
                </tr>
              </thead>
              <tbody>
                  {{ each students }}
                  <tr>
                    <td>{{ $index }}</td>
                    <td>{{ $value.name }}</td>
                    <td>{{ $value.gender }}</td>
                    <td>{{ $value.age }}</td>
                    <td>{{ $value.hobbies }}</td>
                    <td>
                      <a href="/students/edit?id={{ $value.id }}">编辑</a>
                      <a href="/students/delete?id={{ $value.id }}">删除</a>
                    </td>
                  </tr>
                  {{ /each }}
              </tbody>
</table>
```

