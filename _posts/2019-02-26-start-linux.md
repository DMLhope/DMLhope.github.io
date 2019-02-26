---
layout: post
title: 建站教程
date: 2019-02-26
categories: linux
tags: new
header-img: assets/img/4.jpeg
 
---
## 初次建站教程
### 纪念一下，刚架好网站
  说实话其实根本不知道写啥,这也挺搞笑的费了老大劲把这页面弄好结果不知道干啥...
  
  总结一下心路历程吧...一开始准备用hexo+github来做第一个网站来着，结果nodejs+npm的配置让我一度想放弃，太××坑爹了，这不翻墙网站通不了，国内源地址疯狂报错，翻了墙吧，绕不过代理，还是疯狂报错，ok，你报错没问题我换平台，换成windows，嗯不错网上教程也不少，开始还有点小窃喜，结果还是疯狂报错，凭什么人家都是：这一步>成功>下一步>成功>结束，到我这就是：这一步>Error>百度>Error>google>Error>陷入深深的自我怀疑...
  
  哇！这从linux到windows到linux的过程贼心酸，而且网上的教程mac环境的贼多，对穷逼赤裸裸的嘲讽啊，说真的我感觉如果不买mac这辈子要绕着nodejs走...
  
  在极度缺脑细胞的情况下，想找hexo的代替品，这时Jekyll出现了，相关的配置网上都有这里不过多讲解，毕竟重复造轮子比较浪费时间，这里贴上官网：https://www.jekyll.com.cn/
  里面文档非常有用，这里贴出几个我碰到的坑：
  
  1.安装完ruby后要确认ruby-dev这个包有没有安装，不然gem install命令有时会报错。

2.gem install在linux下最好用sudo，不然鬼知道会在哪翻车。

3.推github仓库的时候一定要用master分支，git_page上有详细说明。

jekyll有很多主题模板可以使用，地址是这个：http://jekyllthemes.org/
有喜欢的可以试着配置，实在觉得没啥好看的那就自己参照官网文档做吧，我是有这个打算来着，但是现在没什么时间，以我这个脑子估计得搞很长时间吧...所以用了一个看上去挺棒的模板地址是：https://github.com/kaeyleo/jekyll-theme-H2O
强推啊！

如果使用模板的话推入github之前最好先删除模板跟目录下 .git 这个文件，然后重新建仓库。

本地执行,初始化仓库 

`git init`

建立master分支，并提交

`git checkout -b master`

`git add .`

`git commit -a -m "start"`

接下来再同步仓库到云端...

写在最后，静下心看报错真的很重要，尤其是在初学的时候，切记不能浮躁，看教程要仔细，切记一目十行，自学编程两三年后有可能还是小白，别急，要沉淀，厚积才能薄发，牢记自己的初心，相信手下敲出来的可以是未来...
