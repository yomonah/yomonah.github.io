---
layout:     post
title:      "css3 动效应用"
date:       2017-7-21 10:00:00
author:     "Mia Yu"
catalog: 	true
tags:
    - css3
---

![](https://yomonah.github.io/img/article-img/css3/car.gif)
![](https://yomonah.github.io/img/article-img/css3/wanzi.gif)

抱歉，用工具生成的gif有点卡，小车的轮子都转不利索了，完整demo可以点击文章最底下的［demo展示中心］。

这两个demo的所有元素和动效都是由html＋css实现的
css动画实现：
```
1.animation: css3新增属性，有多个属性值
例：轮子转动
  &.wheel{
     left:  106px;
     animation:  wheel  0.4s  infinite  linear;  
  }
  @keyframes wheel{
    0%{ 
      top: -23px;
      transform:rotate(0deg);
      width: 35px;
    }
    100%{ 
      top: -25px;
      transform:rotate(360deg);
      width: 38px;
    }
}
说明：wheel是animation指定的动画名称
     infinite表示动画播放无限次
     linear指定动画从头至尾速度相同
     在@keyframes中指定动画周期中每个时间段具体的动画效果，动画周期时段可由百分比控制，也可由from、to来表示。
```

```
2. transition: css3属性，处理动效的过渡效果
例：渐变效果
.change{
  opacity: 0;
  transition: opacity 1s;
}
说明：
  transition-property 指定过渡的效果元素，如：width，height，opacity等
  transition-duration 表示过渡的周期（秒／毫秒），如上述例子的1s
  transition-timing-function 规定速度效果的速度曲线
  transition-delay  规定动效的开始时间
```

剩下的一些无非是对于元素的旋转、缩放等处理，用transform等属性即可实现。

小丸子demo：https://yomonah.github.io/project/app.html#/wanzi

旅行小车demo：https://yomonah.github.io/project/app.html#/car

小丸子源码：https://github.com/yomonah/react-demo/tree/master/src/components/wanzi

旅行小车源码：https://github.com/yomonah/react-demo/tree/master/src/components/car