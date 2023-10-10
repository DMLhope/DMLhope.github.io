---
layout: post
title: react学习笔记1
date: 2021-05-05
categories: note react
tags: react
cover: '../../../assets/img/20210505.jpg'
---

## react 简介

React 是一种开源框架，用于创建用户界面。 它最常用于创建 Web 应用程序。 不过，我们可以通过 React Native 使用 React 生成移动或桌面应用程序。 React 主要处理

[模型-视图-控制器](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)
中的“视图”部分。 因此，你可以对路由、管理状态以及访问 API 使用其他库。

## 从头创建react项目（[参考文档](https://medium.com/@JedaiSaboteur/creating-a-react-app-from-scratch-f3c693b84658)）

一组 JavaScript 构建工具链通常由这些组成：

* 一个 package 管理器，比如 [Yarn](https://yarnpkg.com/) 或 [npm](https://www.npmjs.com/)。它能让你充分利用庞大的第三方 package 的生态系统，并且轻松地安装或更新它们。
* 一个打包器，比如 [webpack](https://webpack.js.org/) 或 [Parcel](https://parceljs.org/)。它能让你编写模块化代码，并将它们组合在一起成为小的 package，以优化加载时间。
* 一个编译器，例如 [Babel](https://babeljs.io/)。它能让你编写的新版本 JavaScript 代码，在旧版浏览器中依然能够工作。
此文档主要是讲解如何自己尝试创建一个create react app工具。

### 初始设置（setup）

开始，为react app创建一个目录，然后用  `npm init` 初始化该目录，

```plain
mkdir own-react-project
cd own-react-project
npm init
ls
mkdir public src
git init .
vim .gitignore
```
我们的公共目录将处理任何静态资产，最重要的是将我们的index.html文件置于索引，这将利用渲染您的应用程序。以下代码从React文档中源于一些非常略微的修改。随意将以下HTML标记复制到公共目录中的新文件index.html中。
```plain
<!-- sourced from https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html -->
	<!DOCTYPE html>
	<html>
	
	<head>
	  <meta charset="UTF-8" />
	  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	  <title>React Starter</title>
	</head>
	
	<body>
	  <div id="root"></div>
	  <noscript>
	    You need to enable JavaScript to run this app.
	  </noscript>
	  <script src="../dist/bundle.js"></script>
	</body>
	
	</html>
```
要注意的最重要的是第12行，它和我没react的源程序挂钩，第14行，引用我们的（很快）建立的React应用程序。您可以将构建的脚本命名为您喜欢的内容，但我将使用本教程的Bundle.js。
现在我们已经设置了 HTML 页面，我们可以开始认真对待了。我们将需要设置更多的东西。首先，我们需要确保我们编写的代码可以编译，所以我们需要 Babel。

### Babel

继续运行  

```plain
npm install --save-dev @babel/core@7.1.0 @babel/cli@7.1.0 @babel/preset-env@7.1.0 @babel/preset-react@7.0.0
```

babel-core 是主要的 babel 包——我们需要它让 babel 对我们的代码进行任何转换。 babel-cli 允许你从命令行编译文件。 [preset-react](https://babeljs.io/docs/en/babel-preset-react) 和 [preset-env](https://babeljs.io/docs/en/babel-preset-env) 都是转换特定风格代码的预设——在这种情况下，env 预设允许我们将 ES6 转换为更传统的 javascript，而 react 预设也做同样的事情，但用 JSX 代替。

在项目根目录中，创建一个名为 [.babelrc](https://babeljs.io/docs/en/config-files) 的文件。在这里，我们告诉 babel 我们将使用 env 和 react 预设。

```plain
{
	  "presets": ["@babel/env", "@babel/preset-react"]
}
```

Babel还有大量可用的插件，如果你只需要转换特定的特性，或者你需要的某些特性没有被env覆盖，可以使用这些插件。我们现在不担心这些，但你可以在[这里查看](https://babeljs.io/docs/plugins)。

### webpack

现在我们需要获取并配置Webpack。我们还需要几个包，您需要将它们保存为开发依赖项: 

```plain
npm install --save-dev webpack@4.19.1 webpack-cli@3.1.1 webpack-dev-server@3.1.8 style-loader@0.23.0 css-loader@1.0.0 babel-loader@8.0.2
```
WebPack使用[Loader](https://webpack.js.org/loaders)来处理捆绑的不同类型的文件。它还可以轻松地与开发服务器一起工作，我们将用于在开发中的React项目中服务，并重新加载浏览器页面（已保存的）更改对我们的React组件。为了利用此类，我们需要将WebPack配置为使用我们的装载机并准备DEV服务器。
在项目的根目录下创建一个名为webpack.config.js的新文件。这个文件导出一个带有webpack配置的对象。

```plain
const path = require("path");
	const webpack = require("webpack");
	
	module.exports = {
	  entry: "./src/index.js",
	  mode: "development",
	  module: {
	    rules: [
	      {
	        test: /\.(js|jsx)$/,
	        exclude: /(node_modules|bower_components)/,
	        loader: "babel-loader",
	        options: { presets: ["@babel/env"] }
	      },
	      {
	        test: /\.css$/,
	        use: ["style-loader", "css-loader"]
	      }
	    ]
	  },
	  resolve: { extensions: ["*", ".js", ".jsx"] },
	  output: {
	    path: path.resolve(__dirname, "dist/"),
	    publicPath: "/dist/",
	    filename: "bundle.js"
	  },
	  devServer: {
	    contentBase: path.join(__dirname, "public/"),
	    port: 3000,
	    publicPath: "http://localhost:3000/dist/",
	    hotOnly: true
	  },
	  plugins: [new webpack.HotModuleReplacementPlugin()]
	};
```

让我们快速浏览一下：[entry](https://webpack.js.org/configuration/entry-context/#entry)(入口)（第 5 行）告诉 Webpack 我们的应用程序从哪里开始以及从哪里开始捆绑我们的文件。 接下来这行让 webpack 知道我们在开发模式（development）下工作——这使我们不必在运行开发服务器时添加模式标志。

[modle](https://webpack.js.org/configuration/module)（模块）对象有助于定义导出的 javascript 模块如何转换以及根据给定的规则数组（[rules](https://webpack.js.org/configuration/module#module-rules)）包含哪些模块。

我们的第一条规则就是转换 ES6 和 JSX 语法。 [test](https://webpack.js.org/configuration/module#rule-test) 和 [exclude](https://webpack.js.org/configuration/module#rule-exclude) 属性是匹配文件的条件。 在这种情况下，它将匹配   `node_modules`    和  `bower_components`  目录之外的任何内容。 由于我们还要转换  `.js`  和 . `jsx`  文件，因此我们需要引导 Webpack 使用 Babel。 最后，我们指定要在选项（[options](https://webpack.js.org/configuration/module#rule-options-rule-query)）中使用 env 预设。

下一个规则是处理CSS。因为我们没有对CSS进行预处理或后处理，所以我们只需要确保将样式加载器和CSS加载器添加到use属性。css加载器需要样式加载器才能工作。当只使用一个加载器时，Loader可以用use属性的缩写。

[resolve](https://webpack.js.org/configuration/resolve)属性允许我们指定Web包将解析的扩展-这允许我们导入模块而无需添加其扩展。







