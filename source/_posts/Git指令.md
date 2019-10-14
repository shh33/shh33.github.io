title: Git操作指令
tags:
  - Git
categories:
  - Git
date: 2019-09-30 17:15:00
---
```
git log
```

该命令显示从最近到最远的提交日志。每一次提交都有对应的 commit id 和 commit message。

```
git log --pretty=oneline
```

 参数有序显示

```
git reset --hard id
```

回退应版本 一般取前6位即可

```
git push origin HEAD --force
```

```
git push -f
```

强制回退远程仓库到当前版本
推送到本地到远程仓库：让远程仓库代码和你本地一样，到当前你本地的版本。

```
git reflog
```


定义：查看命令操作的历史

1、做了部分修改，觉得改错了，回退回修改前的状态：（回退到当前版本的初始状态）

```
git reset --hard HEAD
```

2、回退到当前版本的前一个版本

```
git reset --hard HEAD^
```

3、回退到当前版本的上上个版本

```
git reset --hard HEAD^^
```

4、回退到当前版本之前的100个版本

```
git reset --hard HEAD~100
```

