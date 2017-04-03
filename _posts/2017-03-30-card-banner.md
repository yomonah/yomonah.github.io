---
layout:     post
title:      "原生js－仿蘑菇街翻牌轮播组件"
date:       2017-3-30 19:20:00
author:     "Mia Yu"
catalog: 	true
tags:
    - js
---

![](https://yomonah.github.io/img/card-banner/card.gif)

逛蘑菇街的时候看到这个效果的轮播图，就尝试着用react写了个这种效果的组件，用工具录下来的gif图有点卡，看起来不够流畅。

动效主要运用css3的animation、keyframes
配置比较简单，只需要传：
```
data:数据源，仅支持[[{},{},{}],[{},{},{}],...[{},{},{}]]的格式
activeIndex: 默认初始化开始翻牌轮播的索引
duration: 隔多长时间进行一次翻牌轮播，数值型，单位是秒
transitionDuration: 每次翻牌的动画时长，数值型，单位是秒
```

做完以后发现一个大问题，图片加载有些迟缓，翻牌效果就会不流畅，因为我放了超高清大图，后来调整了图片大小，尽量压缩图片，效果就好一些了，不过初次在浏览器中打开，图片尚未缓存时，还是会有些不流畅，上网查了下图片优化方案：
>压缩图片
实用矢量图代替位图
不同场景选择合适的图片格式
图片懒加载
图片预加载

根据我的业务场景，需要将图片做预加载处理，有点忙，以后再做优化。

demo展示中心：https://yomonah.github.io/project/app.html#/card-banner

源码：https://github.com/yomonah/react-demo/tree/master/src/components/card_banner