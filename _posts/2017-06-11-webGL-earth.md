---
layout:     post
title:      "webGL－3D贴图"
date:       2017-6-11 13:30:00
author:     "Mia Yu"
catalog: 	true
tags:
    - webGL
---

![](https://yomonah.github.io/img/article-img/webGL/tietu.gif)
![](https://yomonah.github.io/img/article-img/webGL/earth.gif)
上面两个例子都是应用webGL3D模型贴图实现的

按照上一篇介绍的步骤：
1、先初始化场景、光源、物体
2、创建材质，在材质上添加贴图，再把材质添加到物体上，具体代码：
```
let img = require('../../img/earth.jpg');
let material = new THREE.MeshPhongMaterial({ map: THREE.ImageUtils.loadTexture(img)});
box = new THREE.Mesh(geometry, material );
```
这样就可以实现最基本的贴图功能了

demo1源码：https://github.com/yomonah/react-demo/tree/master/src/components/webGL_img

demo2源码：https://github.com/yomonah/react-demo/tree/master/src/components/webGL_earth