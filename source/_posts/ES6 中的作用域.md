title: ES6中的作用域
author: shh33
categories:
  - ES6
typora-root-url: ..
tags:
  - 作用域
date: 2019-08-28 16:59:00
password:
top:
---

#  ES5 中作用域

```javascript
var callbacks = []
for (var i = 0; i <= 2; i++) {
​    callbacks[i] = function() {
​        return i * 2
​    }
}

console.table([
​    callbacks[0](),
​    callbacks[1](),
​    callbacks[2](),
])
```

![1566975940391](/images/1566975940391.png)

# ES6 中作用域

```javascript
const callbacks2 = []

for (let j = 0; j <= 2; j++) {
​    callbacks2[j] = function() {
​        return j * 2
​    }
}

console.table([
​    callbacks2[0](),
​    callbacks2[1](),
​    callbacks2[2](),
])
```

  块作用域 

![1566975957624](/images/1566975957624.png)

#  立即执行函数

```javascript
((function() {

​    const foo = function() {
​        return 1
​    }
​    console.log("foo()===1", foo() === 1)
​    ;((function() {
​        const foo = function() {
​            return 2
​        }
​        console.log("foo()===2", foo() === 2)
​    })())
})())
```

![1566976525768](/images/1566976525768.png)

```javascript
{
    
​    function foo() {
​       return 1
​    }

​    console.log("foo()===1", foo() === 1)
​    {
​        function foo() {
​            return 2
​        }
​        console.log("foo()===2", foo() === 2)
​    }
​    console.log("foo()===1", foo() === 1)

}
```

![1566976637624](/images/1566976637624.png)

