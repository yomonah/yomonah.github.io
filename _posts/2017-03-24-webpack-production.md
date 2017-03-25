---
layout:     post
title:      "webpack生产环境打包配置"
date:       2017-3-24 15:30:00
author:     "Mia Yu"
catalog: 	true
tags:
    - webpack/node
---

之前写的webpack-dev-server搭建前端工程里面的配置是只针对开发环境的，现在针对生产环境另写了一套配置，配的比较简单，纯属个人浅见，做点笔记。
首先看package.json文件：
```
"scripts": {
    "build": "webpack",
    "dev": "webpack-dev-server --devtool eval --progress --colors --hot --inline --content-base build",
    "dist": "webpack --progress --profile --colors --config webpack.production.config.js"
  },
```
dev是针对开发环境的配置，对应配置文件是webpack.config.js
现在新增了dist，它是针对生产环境的配置，对应配置文件我写在了webpack.production.config.js
1.文件首先引入一些需要的包：
```  
var webpack = require('webpack');
var path = require('path');
var HtmlWebpackPlugin = require('html-webpack-plugin');
```

2.入口文件设置：
```
entry:{
  app:path.resolve(__dirname,'./src/app.js'),
  //将一些第三方的js单独打包在vendors.js 
  vendors:['d3','react']
  },
```

3.配置插件项plugins:
```
plugins: [
  //压缩代码
  new webpack.optimize.UglifyJsPlugin({minimize:true}),  
  //把入口文件vendors数组指定的第三方包打包成verdors.js
  new webpack.optimize.CommonsChunkPlugin('vendors','vendors.js'),
  //用于生成html文件，可定义多个 
  new HtmlWebpackPlugin({
    title:"react-demo",
    filename:'app.html',
    template:'./build/index.html'      //Load a custom template 可以套用你自定义的模版
    })
  ],
```

4.入口文件输出配置：
```
output:{
  path: path.resolve(__dirname,'./dist'),  //指定打包到dist文件
  filename: 'bundle.js'
  }
```

其余配置与webpack.config.js相比，只需要删除devServer相关的配置，其他基本一致。
配置完成以后，执行
>npm run dist

项目中就会生成dist文件用于项目部署，里面包括图片，bundle.js, ventors.js以及html
具体demo可以参见：https://github.com/yomonah/react-demo