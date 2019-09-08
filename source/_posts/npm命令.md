---
title: npm命令
typora-root-url: ..
date: 2019-09-04 20:17:13
tags: npm
categories: npm
password:
top:
---

### npm 常用命令

**npmjs**[网站上传包](https://www.npmjs.com)

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

**如果不想下载可通过下面这个配置**

> ```
> npm config set registry https://registry.npm.taobao.org
> ```
>
> 查看npm 配置信息
>
> ```
> cnpm config list
> ```

### npm 4之后的版本不需要 --save 会自动保存依赖 还会生成一个的lock文件

> package-lock.json文件
>
> 作用
>
> 1. 锁定版本