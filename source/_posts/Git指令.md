title: Git操作指令
tags:

  - Git
categories:
  - Git
date: 2019-09-30 17:15:00
---
```
git config --global user.name "Jack"
git config --global user.email "123@gmail.com"
```

安装 Git 之后，你要做的第一件事情就是去配置你的名字和邮箱，因为每一次提交都需要这些信息：

```
git status
```

该命令显示仓库当前的状态。
```
git diff HEAD -- readme.md
```

该命令可以查看工作区和版本库里面最新版本的区别。
```
git checkout -- readme.md
```

该命令把`readme.md`文件在工作区的修改全部撤销，即让这个文件回到最近一次`git commit`或`git add`时的状态。

```
git clone git@github.com:test/testgit.git
```

该命令拉取项目

```
git branch
```

该命令查看当前分支：

```
git checkout master
git merge dev
```

该命令用于合并指定分支dev到当前分支master

```
git checkout -b dev //等价于以下俩条命令
git branch dev
git checkout dev
```

该命令表示创建`dev`分支，然后切换到`dev`分支

```
git branch -d dev
```

该命令表示合并完成后，删除`dev`分支

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

