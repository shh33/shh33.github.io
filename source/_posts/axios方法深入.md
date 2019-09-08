---
title: axios方法深入
typora-root-url: ..
tags:
  - axios
categories:
  - axios
date: 2019-09-01 16:28:00
password:
top:
---

#     axios实例配置

####     config基本内容

```javascript
axios.create({
      baseURL:'http://localhost:8080',
      timeout:1000,//请求超时时长（ms）
      url:'/data.json',//请求路径
      method:'get', //请求方法post、put、patch、delete
      headers: {
        token: ''
      },//设置请求头
      params:'',//请求参数拼接在url上
      data:''//请求参数放在请求体里
    })
```

####   //1.axios 全局配置  优先级最低

```
axios.defaults.timeout = 1000
axios.defaults.url = 'http://localhost:8080'
```
####   //2.axios 实例配置  优先级中

```
let instance = axios.create()
instance.defaults.timeout = 3000
```

####   //3.axios 请求配置  优先级最高

```
 instance.get('data.json',{
   timeout:6000
 })
```

# 实际开发的用法

```javascript
 let instance = axios.create({
      baseURL:'http://localhost:8080',
      timeout:1000
    })
```

```javascript
instance.get('/testurl',{
  params:{}
}).then((res)=>{
  console.log(res)
})

//用了 baseURL timeout method url params
```
# 拦截器

> #### 在请求或响应贝处理之前拦截它们

####   请求拦截器

```javascript
axios.interceptors.request.use(config=>{
      //在发送请求前做些什么
      return config
    },err=>{
      //在请求错误的时候做些什么
      return Promise.reject(err)
    })
```

#### 响应拦截器

```javascript
 axios.interceptors.response.use(res=>{
      //请求成功对响应数据做处理
      return res
    },err=>{
      //响应错误
      return Promise.reject(err)
    })

  axios.get('/data.json').then((res)=>{
     console.log(res)
   })
```

#### 取消拦截器

```javascript
 let test = axios.interceptors.request.use(config=>{
      config.headers={
          auth:true
      }
      return config
    })
    //取消方法
    axios.interceptors.request.eject(test)
```

#### 实际开发---登入状态（token:''）

```javascript
 let instance = axios.create({})
    instance.interceptors.request.use(config=>{
      config.headers.token = ''
      return config
    })
    //不需要登入的接口
    let newInstance = axios.create({})
```

####   //移动端开发(隐藏弹窗)

```javascript
 let instance_phone = axios.create({})
    instance.interceptors.request.use(config=>{
      $('#mod').show()
      return config
    })
```

```javascript
instance.interceptors.response.use(res=>{
  $('#mod').hide()
  return res
})
```
# 错误处理

```javascript
 let instance = axios.create({})
```

```javascript
 instance.interceptors.request.use(config=>{
      return config
    },err=>{
      //在请求错误的时候做些什么 错误码 401超时 403没找到界面
      $('#modal').show()
      setTimeout(() => {
        $('#modal').hide()
      }, 2000);
      return Promise.reject(err)
 })
```

```javascript
axios.interceptors.response.use(res=>{
  //请求成功对响应数据做处理
  return res
},err=>{
  //响应错误处理 一般http代码500 系统错误 502系统重启
  $('#modal').show()
  setTimeout(() => {
    $('#modal').hide()
  }, 2000);
  return Promise.reject(err)
})
```

```javascript
axios.get('/data.json').then((res)=>{
    console.log(res)
}).catch(err=>{
    console.log(err)
})
```

