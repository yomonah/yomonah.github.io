---
layout:     post
title:      "webGL－入门笔记"
date:       2017-4-9 14:30:00
author:     "Mia Yu"
catalog: 	true
tags:
    - webGL
---

![](https://yomonah.github.io/img/article-img/webGL/webGL-demo.gif)

webGL的3D世界主要由三大要素构成：场景（scene）、相机（camera）和渲染器（renderer），三者缺一不可。渲染的原理是：我们将创建的物体，添加到场景中，再通过相机（可以理解为人的视角）渲染到渲染器，从而呈现在网页中。three.js是webGL一款比较热门的类库，本文以"three.js": "^0.77.1"版本为例，通过网上教程和自身实践整理成这篇笔记。

1.场景(scene)
场景就是所有物体的容器，只需创建一个。假设我们要显示一个苹果，那么就将苹果加入到场景中即可，多个物体可加入到一个场景。
构造函数：
```
var scene = new THREE.Scene();
```

2.相机(camera)
相机决定了场景中哪个角度的景色会显示出来，就像人的视角，分为正投影相机(THREE.OrthographicCamera)和透视投影相机(THREE.PerspectiveCamera)，正投影和透视投影的区别是：透视投影有一个基本点，就是远处的物体比近处的物体小，一般我们采用透视投影相机的情况比较多。
构造函数：
```
//正投影相机
var camera = new THREE.OrthographicCamera(left, right, top, bottom, near, far);
//参数详解：
//left：左平面距离相机中心点的垂直距离
//right：右平面距离相机中心点的垂直距离
//top：顶平面距离相机中心点的垂直距离
//bottom：底平面距离相机中心点的垂直距离
//near：近平面距离相机中心点的垂直距离
//far：远平面距离相机中心点的垂直距离
```
```
//透视投影相机
var camera = new THREE.PerspectiveCamera(fov, aspect, near, far)
//参数详解：
//视角fov：可以理解为视角的大小，如果设置为0，相当于没有了视角，什么也看不到；如果为180，那么可以认为你的视界很广阔，但在180度的时候，往往物体很小，因为物体在你整个可视区域中的比例变小了
//近平面near：表示近处的裁面的距离，也可以认为是眼睛到近处的距离，不能为负数
//远平面far：表示远处的裁面的距离
//纵横比aspect：实际窗口的纵横比，即宽度除以高度，这个值越大，说明宽度越大
```

3.渲染器(renderer)
渲染器决定了渲染结果应挂接在页面的什么元素上，并以怎样的方式绘制。
构造函数：
```
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);//设置渲染区域大小
document.body.appendChild(renderer, domElement);//渲染在domElement并挂接到body下
renderer.render(scene, camera); //将场景通过相机视角渲染出来
```
如果要让物体动起来，那么我们可以利用循环渲染：requestAnimationFrame

4.光源
光是我们看见物体的关键，用Light表示，是所有光源的基类，底下还有很多分类，我举几个最常用的：

环境光：环境光是经过多次反射惹来的光，无法确定其最初的方向，是一种无处不在的光。环境光源放出的光线被认为来自任何方向。因此，当你仅为场景设定环境光时，所有的物体无论法向量如何，都将表现为同样的明暗程度。
构造函数：
```
THREE.AmbientLight(hex); //hex为一个16进制的颜色值
```

平行光：是一组没有衰减的平行的光线，类似太阳光的效果
```
THREE.DirectionalLight(hex, intensity)
```

点光源：由这种光源放出的光线来自同一点，且方向辐射自四面八方
```
THREE.PointLight(color, intensity, distance)；
//color代表光的颜色
//intensity：代表光的强度，默认1.0，表示100%强度的灯光
//distance：代表光的距离，从光源所在的位置，经过distance这段距离之后，光的强度将从Intensity衰减为0，默认0.0，表示光源强度不衰减
```

聚光灯：这种光源的光线从一个椎体中射出，在被照射的物体上产生聚光的效果
```
THREE.SpotLight(hex, intensity, distance, angle, exponent)
//angle：聚光灯着色的角度，用弧度作为单位，这个角度是和光源的方向形成的角度
//exponent：光源模型中，衰减的一个参数，越大衰减越快
```

5.物体
创建一个物体可以包含多种元素，几何体，材质，纹理等，创建一个小球的简单示例：
```
let geometry =new THREE.SphereGeometry(3, 16, 16);   //球体
let material = new THREE.MeshPhongMaterial({color:0x48D1CC,specular:0xffffff,shininess:100});     //材质
var ball = new THREE.Mesh(geometry, material); //两者共同组成一个球体
scene.add(ball); //将球体添加至场景中
```
关于几何体，材质等种类非常多，具体可以参考[three.js源码]：https://github.com/mrdoob/three.js/

6.动画
总结上述步骤：
```
创建场景、相机、渲染器
创建光源
创建物体并添加至场景中
渲染出场景
```
这样就构成了一个完整的但也是最基础的流程，网页中能看到我们创造的物体，接下来说到动画，3D世界中的运动方式总结为三种：移动，旋转和缩放。
运动是相对的，让场景动起来有两种方式：
1). 物体在坐标系中移动，相机不动
```
function animate(){
  ball.position.x += 1;
  renderer.render(scene, camera);
  requestAnimationFrame(animation);
}
```
2). 相机在坐标系中移动，物体不动
```
function animate(){
  camera.position.x += 1;
  renderer.render(scene, camera);
  requestAnimationFrame(animation);
}
```

demo展示中心：https://yomonah.github.io/project/app.html#/webGL-icosahedron

源码：https://github.com/yomonah/react-demo/tree/master/src/components/webGL_ball