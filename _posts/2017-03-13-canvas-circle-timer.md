---
layout:     post
title:      "canvas实现环形倒计时"
date:       2017-3-13 19:15:00
author:     "Mia Yu"
catalog: 	true
tags:
    - canvas
---
之前项目中有做过一款环形计时器，当时是纯用css3实现的，动画效果不错，但有一个非常致命的缺点：通用性差，动画时长只能在css中写死，如果遇到需要统计不同时长的情况下，就必须根据不同的时长写不同的样式。
![](https://yomonah.github.io/img/article-img/circle-time/demo1.gif)

所以现在我换用js和canvas实现环形计时器并将其封装成组件，我们调用这个组件时，只需要传一些配置属性，就可以根据不同需求来展示，非常灵活又实用，具体配置如下：
> let props={
  width:100,  //cavas画布宽度
  height:100,  //画布高度
  radius:20,  //计时器的半径
  time:10*1000,  //需要倒计的时长
  ringColor:'#999',  //进度条的颜色
  defaultColor:'#333' ,  //默认底色
  lineWidth: 5  //进度条的宽度
 }

 具体实现代码可以访问：https://github.com/yomonah/react-demo/tree/master/src/components/circle_timer/circle_timer1

 基于这个计时器我还写了另一个组件，类似于音乐播放器的效果，可以手动开始／暂停：
 ![](https://yomonah.github.io/img/article-img/circle-time/demo2.gif)

配置信息基本是一致的，详细代码可以访问：
https://github.com/yomonah/react-demo/tree/master/src/components/circle_timer/circle_timer2

我的github上会不定时更新一些小组件，感兴趣的可以克隆下来玩玩：
https://github.com/yomonah/react-demo