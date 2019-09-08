---
title: ES6中的常量写法
author: shh33
categories:
  - ES6
tags:
  - 常量写法
date: 2019-08-28 16:59:00
password:
top:
---

#  ES5 中常量的写法



```javascript
Object.defineProperty(window, "PI2", {
​    value: 3.1415926,
​    writable: false,
})
```

console.log(window.PI2)

#   ES6 的常量写法

```javascript
const PI = 3.1415926
```

console.log(PI)

