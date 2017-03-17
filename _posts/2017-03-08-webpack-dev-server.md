---
layout:     post
title:      "webpack-dev-server搭建前端服务器"
date:       2017-3-8 20:59:00
author:     "Mia Yu"
catalog: 	true
tags:
    - webpack/node
---

前端时间用react+webpack搭建套web前端工程，是用webpack-dev-server起的node服务进行开发，通过自己的实践和网上查阅的资料，整理成这篇笔记：

webpack-dev-server是一个小型的Node.js Express服务器，生存在内存中，十分小巧，它使用webpack-dev-middleware来服务于webpack的包，除此自外，它还有一个通过Sock.js来连接到服务器，实现实时编译.
当然，我们先要在工程中安装webpack以及webpack-dev-server包：
```
npm install webpack
npm install webpack-dev-server
```

接下来介绍下webpack-dev-server两种自动刷新模式：

1. iframe模式：页面放在iframe中，当发生改变时重载.
使用iframe模式的话，只需要在访问的URL中添加/webpack-dev-server：  
>http://localhost:8080/webpack-dev-server/index.html

2. inline模式：将webpack-dev-server的客户端入口添加到总的包中
使用inline模式的话访问的URL格式无需改变，它有两种配置形式可以实现：

1. 在webpack.config.js文件中添加：
```
devServer:{
  inline:true,
hot:true,
  port:3000,
}
```
2. 在package.json文件中的scripts（解释下scripts这个对象，它里边可以指定项目在不同 阶段需要执行的命令，以key, value的形式）指定配置：
```
"scripts": {
  "dev": "webpack-dev-server --devtool eval --progress --colors --hot --inline --content-base build"
}
```
我采用的是inline模式，详细配置可以参照我的github:https://github.com/yomonah/react-demo

上述配置中，hot代表启用热模块替换，所谓热模块替换是指我们在开发过程中，一旦前端代码有任何改动，会实时表现在浏览器中而无需手动刷新，这大大节约了开发效率和时间成本。以我的react项目为例，如果启动热模块替换的话，还需要安装一个包：react-hot-loader

其他一些配置选项：

1. --cotent-base <file>: 指定内容的基本路径,例：--content-base bundle
2. --compress: 使用gzip压缩
3. --host <hostname/ip>: 主机名或ip
4. --port <number>: 设置端口号
5. --https: 通过https协议提供webpack-dev-server，包括在提供请求是使用的自签名证书

更多详细文档请参考webpack-dev-server官网：http://webpack.github.io/docs/webpack-dev-server.html#webpack-dev-server-cli