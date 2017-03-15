## 一、准备工作
安装node.js, npm(现在的node版本已整合npm，无需额外安装), webpack

## 二、新建项目文件夹： react-demo
在react-demo中创建一个package.json用于配置项目所需的各种模块，内容如下：
```
{
  "name": "react-demo",
  "version": "0.0.1",
  "description": "",
  "main": "server.js",
  "dependencies": {
    "babel-runtime": "^6.5.0",
    "react": "^0.14.8",
    "react-dom": "^0.14.7"
  },
  "devDependencies": {
    "babel": "^5.2.17",
    "babel-eslint": "^3.1.1",
    "amazeui-react": "^1.0.1",
    "babel-core": "^6.7.4",
    "babel-loader": "^6.2.4",
    "babel-preset-es2015": "^6.6.0",
    "babel-preset-es2016": "^6.0.8",
    "babel-preset-react": "^6.5.0",
    "css-loader": "^0.23.1",
    "less-loader":"2.2.3",
    "material-ui": "^0.15.0-alpha.2",
    "react-hot-loader": "^1.3.0",
    "react-tap-event-plugin": "^0.2.2",
    "style-loader": "^0.13.1",
    "url-loader": "^0.5.7",
    "webpack": "^1.12.14",
    "webpack-dev-server": "^1.14.1",
    "uuid":"^2.0.1"
  },
  "scripts": {
     "build": "webpack",
     "start": "node server.js",
     "dev": "webpack-dev-server --devtool eval --progress --colors --hot --inline --content-base build"
  },
  "author": "mia yu",
  "license": "ISC"
}
```
创建完毕后，在该文件夹下的命令窗口执行：npm install,下载项目需要的包。

这里会碰到一个问题：有些包国内没有资源，需要翻墙下载，这时我们可以使用淘宝镜像解决，主要有以下三种解决方案：
1.通过config命令：
```
npm config set registry https://registry.npm.taobao.org
npm info underscore
```
2.命令行指定
```
npm -registry https://registry.npm.taobao.org info underscore
```
3.编辑~/.npmc加入内容
```
registry = https://registry.npm.taobao.org
```

## 三、配置webpack
通过上述两个步骤之后，我们需要将react-demo工程文件构建成如下结构：
```
app(file)
  components(file)  //编写组建
  main.js  //主入口文件
build(file)
  build.js  //打包入口文件
  index.html
node_modules(file)
package.json
webpack.config.js  //webpack配置文件
```

接下来对webpack.config.js文件进行配置,代码如下：
```
/**
* Created by mia.yu on 2016/6/26.
* 配置打包文件
*/

var webpack = require('webpack');
var path = require('path');

module.exports = {
  //插件项
  plugins: [
      new webpack.NoErrorsPlugin()
  ],

  //页面入口文件配置
  entry:[
      'webpack/hot/dev-server',
      path.resolve(__dirname,'./app/main.js'),
  ],

  //入口文件输出配置
  output:{
      path: path.resolve(__dirname,'./build'),
      filename: 'build.js'
  },

  module: {
     //加载器配置
     loaders: [
        //LESS文件先通过less-load处理成css，然后再通过css-loader加载成css模块，最后由style-loader加载器对其做最后的处理，
        {test: /\.less/, loader: 'style-loader!css-loader!less-loader'},
        {test: /\.css$/, loader: 'style-loader!css-loader' },

        //.js 文件使用 jsx-loader 来编译处理 jsx-loader使其支持ES6语法
        {test: /\.js$/,
          exclude: /node_modules/,
          loader: 'babel',
        query:{
          presets:['es2015','react']
        } //备注：es2015用于支持ES6语法，react用于解决render()报错的问题
    },

    //.scss 文件使用 style-loader、css-loader 和 sass-loader 来编译处理
    {test: /\.scss$/, loader: 'style!css!sass?sourceMap'},

    //图片文件使用 url-loader 来处理，小于8kb的直接转为base64
    {test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
  ]
},

//其它解决方案配置
resolve: {
  //查找module的话从这里开始查找
  //root: 'E:/github/flux-example/app', //绝对路径
  //自动扩展文件后缀名，意味着我们require模块可以省略不写后缀名
  extensions: ['', '.js', '.json', '.scss','jsonp','less','.jsx'],

  //模块别名定义，方便后续直接引用别名，无须多写长长的地址
  alias: {
    AppStore : 'js/stores/AppStores.js',
    ActionType : 'js/actions/ActionType.js',
    AppAction : 'js/actions/AppAction.js'
  }
},
  devServer:{
    inline:true,
    port:8080,  //项目访问端口号
  }
};
```
在工程目录下执行webpack命令进行大包，打包完后就会在build目录中出现build.js文件，编译成功。build.js是整个工程的入口文件，需要将其引用在index.html，工程才可正常运行。

index.html文件如下：
```
<!DOCTYPE html>
<html lang='en'>
<head>
  <meta charset='utf-8'>
  <title>React Demo</title>
</head>
<body>
  <div id='content'></div>
  <script src='build.js'></script>
</body>
</html>
```

## 四、启动项目
做好以上三个步骤后，一个简单的react＋webpack项目便构建成功，输入命令：npm run dev 启动工程，打开 http://localhost:8080 就可访问工程了。