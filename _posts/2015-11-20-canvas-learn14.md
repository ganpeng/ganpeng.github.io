---
layout: post
title:  canvas-learn-14
tags: [javascript]
---

<h1 style="text-align:center;">Canvas API</h1>

### canvas上下文

> 每个canvas元素都包含一个绘图上下文，通过这个上下文(context)就可以访问绘图API

<pre>
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d');
</pre>

### 使用clearRect消除图案

> 在大多数的动画中，必须在绘制下一帧图案前清除canvas,正是通过这一手段模拟出物体正在运动的效果，通过绘制图案，擦出它，然后将其绘制到另一个位置，这样就可以把一系列图像模拟成一个物体发生了移动

<pre>
    context.clearRect(0, 0, canvas.width, canvas.height);
</pre>

### 设置线条的外观

> 绘图上下文包含了一系列可以用于更改随后绘制的线条的外观的属性：

> * strokeStyle : 该属性用于指定线条的颜色，该值可以是一个颜色值，一个渐变对象或者一个模式对象，默认为黑色('#000');
* lineWidth : 该属性用于指定线条在其路径上的宽度，当属性值为1时，该线条会在其路径的两侧分别延伸出半个像素，无法将其线条绘制在其路径的内部或外部，该属性必须为正值；
* lineCap : 用来控制线条的终点，属性值包含：butt, round, square,默认值为butt;
* lineJoin : 决定两条相连的线段如何结合，或者连接线的弯头部分如何绘制，该属性值包含round, bevel, miter选项，默认为miter
* miterLimit : 当lineJoin属性设置为miter时， 该属性可用于控制两条相交线外侧交点与内侧交点的距离，它必须是大于零的有限数，默认为0；