---
 title: axios的使用方法
 author: shh33
 tags:
  - ajax
  - axios
 categories:
  - axios
  - ajax
 date: 2019-08-29 13:50:00
 password:
 top:
 typora-root-url: ..
---

# axios请求方法

> 1. get: 获取数据
> 2. post: 提交数据（表单提交+文件上传）
> 3. put: 更新数据（所有数据推送到后端）
> 4. patch: 更新数据（只将修改的数据推送到后端）
> 5. delete: 删除数据

### 具体由后端定义

### 1.get方法的使用

```javascript
 created() {
   axios.get('/data.json').then((res)=>{
     console.log(res)
   })
 }
```

```javascript
axios({
     method:'get',
     url:'/data.json',
   }).then((res)=>{
     console.log(res)
   })
```

> **请求id=12**

```javascript
created() {
   axios.get('/data.json',{
       params:{
       id:12
     }
   }).then((res)=>{
     console.log(res)
   })
```

```javascript
axios({
     method:'get',
     url:'/data.json',
     params:{
       id:12
     }
   }).then((res)=>{
     console.log(res)
   })
```

> **http://localhost:8080/data.json?id=12**请求地址

### 2.post方法的使用

```javascript
axios.post('/post',{},config) 三参数
```

> **from-data 表单提交（图片/文件上传）**
>
> **applicition/json**

```javascript
//applicition/json
let data = {
  id:12
}
axios.post('/post',data).then((res)=>{
 console.log(res)      
})
axios({
  method:'post',
  url:'/post',
  data:data
}).then((res)=>{
 console.log(res)
})

//from-data 表单提交（图片/文件上传）
let formData = new FormData()
for(let key in data){
  formData.append(key,data[key])
}
axios.post('/post',formData).then((res)=>{
 console.log(res)      
})
```

 ![1567323056013](/images/1567323056013.png)
 ![1567323129124](/images/1567323129124.png)
 ![1567323172073](/images/1567323172073.png) 

### 3.put 请求

```javascript
   axios.put('/put',data).then((res)=>{
      console.log(res)      
    })
```

![1567323306306](/images/1567323306306.png)![1567323346826](/images/1567323346826.png)

###  4.patch

```javascript
axios.patch('/patch',data).then((res)=>{
     console.log(res)      
    })
```

![1567323403005](/images/1567323403005.png)

### 5.delete(2个参数)

```
axios.delete(url,config)
```

> 第一种
>

```javascript
xios.delete('/delete',{
      params:{
        id:12
      }
    }).then((res)=>{
      console.log(res)
    })
```
```javascript
axios({
      method:'delete',
      url:'/delete',
      params:{
        id:12
      }
    }).then((res)=>{
      console.log(res)
    })
```

![1567324364334](/images/1567324364334.png)

> 第二种

```javascript
axios.delete('/delete',{
      data:{
        id:12
      }
    }).then((res)=>{
      console.log(res)
    })
```

```javascript
axios({
      method:'delete',
      url:'/delete',
      data:{
        id:12
      }
    }).then((res)=>{
      console.log(res)
    })
```

![1567324422875](/images/1567324422875.png)