---
title: vue-router相关知识点
typora-root-url: ..
date: 2019-10-24 16:10:36
tags:
categories:
password:
top:
---

## 关于vue-router的一下知识点总结

<!--more-->

1. 关于路由跳转
   1. 1 要点导包
   2. 2 配置路径

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Clithree from '@/components/Clithree'
import Index from '@/components/Index'
import Three from '@/components/Three'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Index',
      component: Index
    },
    {
      path: '/a',
      name: 'Clithree',
      component: Clithree
    }
  ]
})
```



2. 关于配置子路由

```javascript
{
      path: '/a',
      name: 'Clithree',
      component: Clithree,
      children: [
        {
          path: '/a1',
          name: 'Three',
          component: Three
        }
      ]
    }
```

3. 页面上跳转

   使用`touter-link`标签

```html
<p><router-link to="/">index</router-link></p>
```

4. 关于地址的研究

   4.1 去除#号（微信支付相关的地方#会冲突 但是页面不存在会报404）

```javascript
export default new Router({
  mode: 'history', //hash
  routes: [
    {
      path: '/',
      name: 'Index',
      component: Index
    },
    {
      path: '/a',
      name: 'Clithree',
      component: Clithree,
    }
  ]
})

```

![1571905361513](/images/1571905361513.png)

