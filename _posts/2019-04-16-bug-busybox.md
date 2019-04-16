---
layout: post
title: deepin系统无法正常开机进入busybox的解决方案
date: 2019-04-08
categories: bug
tags: busybox deepin
cover: '../../../assets/img/20190416.jpg'
---

# deepin系统无法正常开机进入busybox的解决方案

这个问题多数情况下是强制断电导致的，但这次我碰上是在磁盘分区之后,也是见了鬼了...


首先回忆起自己安装系统的分区


我的系统装在`/dev/sda2`

所以在busybox环境下执行`fsck /dev/sda2`，之后跟着提示一路回车即可。