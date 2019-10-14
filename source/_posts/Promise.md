---
title: Promise
typora-root-url: ..
date: 2019-09-04 20:17:13
tags: Promise
categories: Promise
password:
top:
---

![1567996038628](/images/1567996038628.png)

# Promise是一个构造函数

![1567997039617](/images/1567997039617.png)

## 链式调用

```javascript

var p1 = new Promise(function (resolve, reject) {
  fs.readFile('./data/a.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p2 = new Promise(function (resolve, reject) {
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p3 = new Promise(function (resolve, reject) {
  fs.readFile('./data/c.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

p1
  .then(function (data) {
    console.log(data)
    // 当 p1 读取成功的时候
    // 当前函数中 return 的结果就可以在后面的 then 中 function 接收到
    // 当你 return 123 后面就接收到 123
    //      return 'hello' 后面就接收到 'hello'
    //      没有 return 后面收到的就是 undefined
    // 上面那些 return 的数据没什么卵用
    // 真正有用的是：我们可以 return 一个 Promise 对象
    // 当 return 一个 Promise 对象的时候，后续的 then 中的 方法的第一个参数会作为 p2 的 resolve
    // 
    return p2
  }, function (err) {
    console.log('读取文件失败了', err)
  })
  .then(function (data) {
    console.log(data)
    return p3
  })
  .then(function (data) {
    console.log(data)
    console.log('end')
  })

```

封装

```javascript
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })

```

## promise应用场景 调用多个接口

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>

<body>
  <form action="" id="user_form">
  </form>
  <script type="text/template" id="tpl">
    <div>
      <label for="">用户名</label>
      <input type="text" value="{{ user.username }}">
    </div>
    <div>
      <label for="">年龄</label>
      <input type="text" value="{{ user.age }}">
    </div>
    <div>
      <label for="">职业</label>
      <select name="" id="">
        {{ each jobs }} {{ if user.job === $value.id }}
        <option value="{{ $value.id }}" selected>{{ $value.name }}</option>
        {{ else }}
        <option value="{{ $value.id }}">{{ $value.name }}</option>
        {{ /if }} {{ /each }}
      </select>
    </div>
  </script>
  <script src="node_modules/art-template/lib/template-web.js"></script>
  <script src="node_modules/jquery/dist/jquery.js"></script>
  <script>
    // 用户表
    //  其中一个接口获取用户数据
    //  职业：2
    // 职业信息表
    //  其中一个接口获取所有的职业信息
      
    //普通的方式
    get('http://127.0.0.1:3000/users/4', function (userData) {
      get('http://127.0.0.1:3000/jobs', function (jobsData) {
        var htmlStr = template('tpl', {
          user: JSON.parse(userData),
          jobs: JSON.parse(jobsData)
        })
        console.log(htmlStr)
        document.querySelector('#user_form').innerHTML = htmlStr
      })
    })

      
    // jQurey中封装的promise
    var data = {}
    $.get('http://127.0.0.1:3000/users/4')
      .then(function (user) {
        data.user = user
        return $.get('http://127.0.0.1:3000/jobs')
      })
      .then(function (jobs) {
        data.jobs = jobs
        var htmlStr = template('tpl', data)
        document.querySelector('#user_form').innerHTML = htmlStr
      })

    // 封装的promise方法
    var data = {}
    pGet('http://127.0.0.1:3000/users/4')
      .then(function (user) {
        data.user = user
        return pGet('http://127.0.0.1:3000/jobs')
      })
      .then(function (jobs) {
        data.jobs = jobs
        var htmlStr = template('tpl', data)
        document.querySelector('#user_form').innerHTML = htmlStr
      })

    pGet('http://127.0.0.1:3000/users/4', function (data) {
      console.log(data)
    })

    pGet('http://127.0.0.1:3000/users/4')
      .then(function (data) {
        console.log(data)
      })

    function pGet(url, callback) {
      return new Promise(function (resolve, reject) {
        var oReq = new XMLHttpRequest()
        // 当请求加载成功之后要调用指定的函数
        oReq.onload = function () {
          // 我现在需要得到这里的 oReq.responseText
          callback && callback(JSON.parse(oReq.responseText))
          resolve(JSON.parse(oReq.responseText))
        }
        oReq.onerror = function (err) {
          reject(err)
        }
        oReq.open("get", url, true)
        oReq.send()
      })
    }


    // 这个 get 是 callback 方式的 API
    // 可以使用 Promise 来解决这个问题
    function get(url, callback) {
      var oReq = new XMLHttpRequest()
      // 当请求加载成功之后要调用指定的函数
      oReq.onload = function () {
        // 我现在需要得到这里的 oReq.responseText
        callback(oReq.responseText)
      }
      oReq.open("get", url, true)
      oReq.send()
    }
  </script>
</body>

</html>

```

