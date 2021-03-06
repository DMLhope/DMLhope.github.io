---
layout: post
title: git 常用命令学习整理
date: 2019-03-21
categories: 常用命令
tags: git
cover: '../../../assets/img/20190321-1.jpg'
---






### git 常用命令学习整理
##### 前言：
主要还是博主太笨，经常性的记不住之前用过的命令，每次都得现查，有点难受...

由于需要的是工作上用到过的，所以不定时增量更新。

想详细学习可以参考廖雪峰老师的git教程，网址：https://www.liaoxuefeng.com/

##### 正文：

2019年3月21日更新：

+  设置你的github的用户名和密码

```
    git config --global user.name "Your Name"
    
    git config --global user.email "email@example.com"
    
 ```
 
 + 给当前目录添加git仓库
 
 ` git init `
 + 把文件添加到暂存区
 
 ` git add 文件名`
 
 + 提交到仓库
 
 ` git commit -m "说明"`
 
 注：上面两个命令最好交叉着用，这个概念大致可以理解为，在执行第一条命令时，相当于你把货物给了仓库管理员，执行第二条命令的时候，仓库管理员会把他手上有的东西，贴上你写的说明标签，放到仓库，所以也可以一次性把很多东西给仓库管理员，然后让他一次全放到仓库里，贴上标签。当然不建议这样用，因为搞不好你就记不得你改哪个文件是为了什么。
 还有一个可以直接让仓库管理员把你手上所有东西一次性贴标签扔仓库的命令` git commit -a -m "说明"` 当然也不建议使用，貌似也不能用。（不建议你写个屁。。。）
 
 + 查看当前仓库状态，比如是否有修改了未提交的文件
 
 ` git status`
 
 + 查看被修改文件的改动处，如果在上面的命令里发现了没提交的修改，你又记不得该哪了，可以用这条命令
  
 ` git diff 文件名`
 
 + 你要查看你提交的历史记录的话，可以用下面这条命令
 
 ` git log`
 
 + 在Git中，用HEAD表示当前版本，也就是最新的提交,上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。所以，想穿越回过去的话可以试试下面两个命令。

``` 
git reset --hard HEAD^

git reset --hard commit号

 ```
 
 注：commit号表示的就是你git log出的各个历史版本的id
 
+ 当你需要从人家的仓库拷一份源码下来时可以用：

` git clone 网址`

+ 查看分支

` git branch`

+ 创建分支

` git branch 分支名`
+ 切换分支

` git checkout 分支名`

+ 创建并切换分支（强推！人身苦短，没有啥特殊情况能少敲点代码就少敲点）

` git checkout -b 分支名`

+ 新建tag

` git tag tag号`
+ 给历史提交的commit打tag

` git tag tag号 commit号`

+ 查看tag

` git tag`
+ 用tag创建一个分支并切换过去（人生苦...啪！闭嘴！）

` git checkout -b 分支名 tag号`

+ 查看tag信息

` git show tag号`

+ 推送远程仓库

` git push`

+ 推送某个tag去远程仓库

` git push origin tag号`
+ 推送所有标签去远程仓库

` git push origin --tags`

