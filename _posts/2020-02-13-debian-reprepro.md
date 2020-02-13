---
layout: post
title: reprepreo基本使用
date: 2020-02-13
categories: debian
tags: reprepreo
cover: '../../../assets/img/20200213-1.jpg'
---

## 仓库说明
deepin使用的是debian的包管理方式

安装与管理软件有两个工具：apt && dpkg

仓库主要是提供软件包给apt进行安装

仓库的主要配置文件在仓库所采目录里的`conf`目录中

其中`distributions`是最主要的配置文件，主要内容如下：
```
Origin: Your project name
Label: Your project name
Codename: <osrelease>
Architectures: i386 amd64
Components: main
Description: Apt repository for project x
SignWith: <key-id>（可选）
```

## reprepo命令的基本使用
### 注意点：

首先确保reprepro命令已被安装：apt install reprepro

reprepro的使用得在仓库所在目录即conf目录所在的目录

#### 基本使用：
+ 导入软件包： reprepro includedeb <osrelease> <debfile> //osrelease即Codename  debfile顾名思义deb的软件包
+ 导入dsc文件： reprepro includedsc <osrelease> <dscfile>
+ 如果按照debian官方的打包规则打出软件包的时候会同时生成一个changes文件，可以通过这个changes文件导入所有源码dsc和deb包：reprepro include <osrelease> <changesfile>
+ 删除软件包（慎用）：reprepro remove <osrelease> <debfile> //debian仓库默认会自动用高版本软件替换低版本软件，所以在导入高版本软件包时需注意是否需要保留低版本软件包，请注意备份，并且推荐使用升级软件包版本号的方式来覆盖仓库中的低版本软件包，并不建议删除软件包

## 参考文档：
[https://wiki.debian.org/DebianRepository/SetupWithReprepro]