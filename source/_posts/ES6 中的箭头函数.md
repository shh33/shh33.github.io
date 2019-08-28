---
title: ES6 的箭头函数
author: shh33
date: 2019-08-28 16:59:27
categories:
password:
typora-root-url: ..
top:
---
# ES3,ES5

```
{

  var evens = [1, 2, 3, 4, 5];

  var odds = evens.map(function(v) {

​    return v + 1

  });

  console.log(evens, odds);

};
```

# ES6

```
{

  let evens = [1, 2, 3, 4, 5];

  let odds = evens.map(v => v + 1);

  console.log(evens, odds);

} 
```

> 1. 箭头函数 function a(){
>
>    ​	() => { }           
>
>     }
>
> 2. function(v)中的有参数直接 提出来
>
> 3. {}中的表达式作为返回值可以直接省略花括号

![1566978448880](/images/1566978448880.png)

# ES3,ES5

######  块作用域

```
{

var factory = function() {

​    this.a = 'a';

​    this.b = 'b';

​    this.c = {

​      a: 'a+',

​      b: function() {

​        return this.a

​      }

​    }

  }

  console.log(new factory().c.b()); //a+

};
```

> 1. this的指向就是该函数被调用的对象
> 2.  c 调用了 b() 所以 c 中的 a 的值就是 a+

```
{

  var factory = function() {

​    this.a = 'a';

​    this.b = 'b';

​    this.c = {

​      a: 'a+',

​      b: () => {

​        return this.a

​      }

​    }

  }

  console.log(new factory().c.b());  //a

}
```

> 1. 箭头函数体中**this**的指向是定义时**this**的指向
>
>    **b**定义时 **this** 指向 函数体中的 **this**
>
>        this.a = 'a';
>        
>        this.b = 'b';
>        
>        this.c = {
>        
>        ​      a: 'a+',
>        
>        ​      b: () => {
>        
>        ​        return this.a
>        
>        ​      }
>        
>        ​    }
>    构造函数的 **this** 指向 **factory** 构造函数的实例 **new factory()**
>
>    **new factory()** 的实例就是 **this.a = 'a'**
>
> 2. 解决this的指向不确定