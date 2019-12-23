---
title: 每日一题-原生实现indexOf
typora-root-url: ..
date: 2019-10-30 11:14:49
tags: JavaScript
categories: JavaScript
password:
top:
---

```javascript
function indexOf(arr, item) {
  if (Array.prototype.indexOf){   //判断当前浏览器是否支持
      return arr.indexOf(item);
  } else {
      for (var i = 0; i < arr.length; i++){
          if (arr[i] === item){
              return i;
          }
      }
  }     
  return -1;     //总是把return -1暴漏在最外层
}
}
```

