---
layout: post
title: nodejs，npm，electron配置环境踩坑记录
date: 2019-03-21
categories: web
tags: electron
cover: '../../../assets/img/20190324.jpg
---



#### nodejs，npm，electron配置环境踩坑记录

开发环境：一个白白嫩嫩的deepin15.9，（别问我为啥要白嫩的，人生苦短，该重来的时候得重来，不然...~~~~(>_<)~~~~）

##### 首先安装nodejs和npm

` sudo apt install nodejs nodejs-dev npm`

(那个dev的包说实话我不知道是干啥的，但是我装了，所以还是记录下来比较好。)

##### 更换npm为cnpm，使用淘宝的镜像

` sudo npm install -g cnpm --registry=https://registry.npm.taobao.org`

这里建议带上` sudo`不然容易报权限上的问题，当然如果你是默认root用户的话就当我没说，但是不建议，早年我也喜欢用root用户，知道有天傻了吧唧的敲了个` rm -rf /`没来的及敲后面的却先按了回车...

貌似这条命令可以直接修改npm的镜像地址`  sudo npm config set registry https://registry.npm.taobao.org`不过我用着好像没什么用...

##### 安装electron

` sudo cnpm install -g electron electron-forge`

直到这一步如果你是个新环境那基本不会有什么问题下面开始可以构建项目了，我比较先手动去构建一个简单的electron项目，参照IT营的免费教学视频，构建过程如下：
首先是创建一个目录：

` mkdir my-electron-app`

` cd my-electron-app`

然后先创建一个` index.html`文件

内容随便，这里我填了一个HTML5的模板：

``` 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    hello electron
</body>
</html>
```

接下来创` main.js`文件，内容如下:

``` 
 //electron对象的引用
 var electron = require('electron');
 var app=electron.app;
 //BrowserWindow类的引用
 var BrowserWindow=electron.BrowserWindow;

 var mainwindow=null;
 //监听应用准备完成的事件
 app.on('ready',function(){
     //创建窗口
     mainwindow=new BrowserWindow({width:400,height:400});
     mainwindow.loadFile('index.html');//选择要打开的主页文件
     mainwindow.on('closed',()=>{//监听了一个关闭事件
         mainwindow=null;
     })
 })
```

然后在命令行里输入` npm init --yes`

之后可以发现多了一个` package.json`文件

内容如下：

``` 
{
  "name": "你的文件夹名",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-preset-env": "^1.7.0"
  }
}
```

尤其要注意，看看你的` main`是否指向` main.js`。

之后就可以运行试试看了：

去吧命令行使用` electron .`命令进行攻击（口袋妖怪bgm起）

好像没什么效果

对方向你使用Error攻击：

``` 
App threw an error during load
Error: Couldn't find preset "env" relative to directory...
```

效果拔群！你的心情变糟了！

这边使用浏览器google，找到链接：https://blog.csdn.net/hzzou/article/details/76650241

去吧命令行，使用链接中的` cnpm install babel-preset-env --save-dev`+ ` electron .`攻击！(就是依次输入这两条命令)

好像有效果了，对方不报之前的错了

对方再次向你使用ERROR攻击：

``` 
App threw an error during load
Error: Couldn't find preset "react" relative to directory ...
```

效果拔群！你的心情变得更糟了！

再次使用浏览器google，找到链接：https://blog.csdn.net/fenglailea/article/details/80068101

去吧命令行，使用链接中的

``` 
npm install react react-dom 
npm install babel-core babel-loader babel-preset-react 
npm install webpack 
electron .
```
攻击！

好像又有效果了，对方不报之前的错了

对方又TM向你扔了个ERROR

``` 
App threw an error during load
Error: Cannot find module 'election'
```

效果拔群！结合你今天之前折腾其他东西抓狂的经历，你已经快崩溃了。

诶？等等，这个不是...哦，我把` main.js`里第一句中的` electron`写成了` election`（你们上面看到的是修改完的船（quan）新版本,所以你们应该不会报错）

改完之后，命令行，` electron .`

效果拔群，对方倒下了，程序运行起来了，你得到了运行起来的简陋的程序和浪费的时间(没有金币，你的命令行也不会加经验)...

你长叹了一口气，关闭了刚跑起来的程序。