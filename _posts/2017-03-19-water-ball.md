---
layout:     post
title:      "d3.js-水波球"
date:       2017-3-19 18:33:00
author:     "Mia Yu"
catalog: 	true
tags:
    - d3.js
---
这款基于d3.js开发的水波球组件，原先是一位大神用jquery写的，我在此基础上，用v4.x版本重新改写并封装成了react组件，运行效果如下：
![](https://yomonah.github.io/img/article-img/water-ball/water_ball.gif)

调用组件的时候，只需要传入config和data两项props，config的配置信息：
```
idDom: 传入容器id,这是必传项，用于指定画布的dom
width和height: 容器的宽高
textColor: 显示在底容器层数据文本的颜色
waveTextColor: 显示在波浪上数据文本的颜色；
    这里需要注意下，为什么要设置两处数据文本颜色，其实是因为虽然水波球中显示的文字看起来只有一处，但其实是两个地方:
    1.当水波浪低于文字位置时，我们看见的文字是由底容器层显示的；
    2.当水波浪高于文字时，底容器的文字会被波浪遮挡，这时我们看到的文字其实是显示在水波浪上的文本
textSize: 文本字体大小
outerCircle: 外层圆的相关配置，包含半径r和填充色fillColor两个属性
innerCircle: 内层圆的相关配置，包含半径r和填充色fillColor两个属性
```

例：
```
let props={
  idDom:'circleWaterBall',
  width:200,
  height:300,
  textColor:"#C2E2F9",
  waveTextColor:"#C2E2F9",
  textSize:0.7,
  outerCircle:{
    r:50,
    fillColor:'#35a1e8'
  },
  innerCircle:{
    r:50,
    fillColor:'rgba(53, 161, 232,0.8)'
   }
  };
```

这里只列举了一些最基本的配置信息，更多配置项可以查看源码

数据data的话，目前支持的格式为：
>data:{id:1, value:0.9}
id用于唯一识别码
value代表数值，范围［0,1]，1代表100%

查看源码请访问:https://github.com/yomonah/react-demo/tree/master/src/components/water_ball