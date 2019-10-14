---
title: Node模块
typora-root-url: ..
tags:
  - Node模块
categories:
  - Node
date: 2019-09-03 18:57:00
password:
top:
---
# 总结

- 模块系统
  
  - 核心模块
    - fs 文件操作模块
    - http 网络服务构建模块
    - os 操作系统信息模块
    - path 路径处理模块
    - url 路径操作模块
  - 第三方模块
    + art-template
    
      1. 安装  npm install art-template
    
      2. 加载  var template = require('art-template') 
    
      3. 使用  template.render()
    
    + 通过npm下载使用
  - 自己写的模块
    
    + 自己创建的文件
  - 加载规则以及加载机制
  - 循环加载
  
- npm

- package.json

- Express
  - 第三方 Web 开发框架
  - 高度封装了 http 模块
  - 更加专注于业务，而非底层细节
  - 知其所以然
  
- 增删改查
  
  - 使用文件来保存数据（锻炼异步编码）
  
- MongoDB
  
  - （所有方法都封装好了

## 什么是模块化

1. 文件作用域
2. 通信规则
   - 加载require
   - 导出exports

## CommonJS模块规范

在node中的JavaScript有个重要的概念：模块系统

- 模块作用域 
- 使用 require方法加载模块
- 使用exports接口对象来导出模块中的成员

### 加载 `require`

语法：

```javascript
var 自定义变量名 = require('模块')
```

作用：

1. 执行被加载模块中的代码

 	2. 得到被加载模块中的``exports``导出的接口对象

### 导出 `exports`

- node中是模块作用域，默认文件中所有的成员只在当前文件模块有效

- 对于希望其他模块访问的成员，需要把公开的成员挂载到 `exports` 接口对象中就可以了

	- 导出多个成员

	```javascript
exports.a = 123
  exports.b = 'hello'
  exports.c = function () {}
  exports.d = {
  	foo : 'bar'
  }
  ```
  
  - 导出单个成员（拿到的是函数或者字符串）
  
  ```javascript
  module.exports = function (x, y) {
    return x + y
  }
  ```
  
  这种情况下面会覆盖前面的
  
  ```javascript
  module.exports = function (x, y) {
    return x + y
  }
  
  module.exports = 'hello'
  ```

### module.exports 和 exports 的区别

- 每个模块中都有一个 module 对象
- module 对象中有一个 exports 对象
- 我们可以把需要导出的成员都挂载到 module.exports 接口对象中
- 也就是：`moudle.exports.xxx = xxx` 的方式
- 但是每次都 `moudle.exports.xxx = xxx` 很麻烦，点儿的太多了
- 所以 Node 为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
- `exports === module.exports` 结果为  `true`s
- 所以对于：`moudle.exports.xxx = xxx` 的方式 完全可以：`expots.xxx = xxx`
- 当一个模块需要导出单个成员的时候，这个时候必须使用：`module.exports = xxx` 的方式
- 不要使用 `exports = xxx` 不管用
- 因为每个模块最终向外 `return` 的是 `module.exports`
- 而 `exports` 只是 `module.exports` 的一个引用
- 所以即便你为 `exports = xx` 重新赋值，也不会影响 `module.exports`
- 但是有一种赋值方式比较特殊：`exports = module.exports` 这个用来重新建立引用关系的

### require 方法加载规则

- 优先从缓存加载 ------main加载a 和 b | a中加载b | main不会加载b了 只有b导出的内容
- 判断模块标识符
  - 核心模块   （只需要名字fs/http/os/url）
  - 路径形式的模块 （.js后缀名可以省略）
  - 第三方模块 (必须npm下载 使用包名加载 )
  - node_modules

### package.json 包描述文件（类似产品说明书）

- 可以通过npm init自动初始化出来
- npm install 包名（建议加上--save）

- dependencies 选项的作用 （保存第三方包的依赖信息）(npm install 找回依赖的包)

### npm 常用命令

npmjs网站上传包

```
npm --version // 查看版本
```

```
npm install --global npm //升级npm
```

```
npm init 
```

 ```
npm init -y //快速生成
 ```

 ```
npm stall 包名 
 ```

>   1. npm i 包名 （简写）
>   2. 只下载
>

 ```
  npm stall 包名 --save 
 ```

>   1. 下载并保存依赖项 生成dependencies 选项
>   2. npm i -S 包名 （简写）
>

 ```
  npm uninstall 包名  //只删除，有依赖项会依然保存
 ```

 ```
  npm uninstall --save 包名
 ```

>   1. 删除的同时去除依赖信息
>   2. npm un -S 包名 （简写）

 ```
  npm help //查看使用帮助
 ```

 ```
  npm 命令 help //查看指定命令的使用帮助
 ```

```
npm install --global cnpm //解决被墙的问题使用cnpm
```

> --global 安装全局 在任意目录都可以
>
> 使用方法执行命令 替换 npm为 cnpm
>
> 如果不想下载可通过下面这个配置
>
> ```
> npm config set registry https://registry.npm.taobao.org
> ```
>
> 查看npm 配置信息
>
> ```
> cnpm config list
> ```

### Express 基本使用

### 301 和 302 的区别

如何在 Node 中实现服务器重定向

- header('location')
  - 301 永久重定向 浏览器会记住
    - a.com b.com
    - a 浏览器不会请求 a 了
    - 直接去跳到 b 了
  - 302 临时重定向 浏览器不记忆
    - a.com b.com
    - a.com 还会请求 a
    - a 告诉浏览器你往 b

