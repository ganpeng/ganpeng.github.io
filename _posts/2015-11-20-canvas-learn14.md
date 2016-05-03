---
layout: post
title:  canvas-learn-14
tags: [canvas]
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

### 使用lineTo与moveTo绘制路径

> lineTo命令接受单个点作为参数：线段的终点；他会把起点和终点的信息保存在一个对象中。
> canvas上下文总是持有一条唯一的当前路径，一条路径可以拥有零条或者多条子路径，每条子路径由一系列通过直线或者曲线相连的点构成，如果一条路径的起点和终点间首尾相连，那么这条路径称为闭合路径。调用context.beginPath()既表示你想开始绘制一条新的路径。一条路径只不过是构成一条线的一系列坐标位置，为了将它渲染到canvas上，需要调用context.stroke()方法。

<pre>
    context.beginPath();
    moveTo(0, 0);
    lineTo(100, 100);
    context.stroke();
</pre>

> 上述代码表示，在canavs上画一条从左上角(0, 0)到(100, 100)的直线，在画完一条线后，这条线的终点将自动成为下一条线的起点，或者可以用context.moveTo方法为下一条线指定一个新的起点.

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        mouse = utils.captureMouse(canvas);

    function mouseMoveHandle(e) {
      context.lineTo(mouse.x, mouse.y);
      context.stroke();
    }

    canvas.addEventListener('mousedown', (e) => {
      context.beginPath();
      context.moveTo(mouse.x, mouse.y);

      canvas.addEventListener('mousemove', mouseMoveHandle, false);
    }, false);

    canvas.addEventListener('mouseup', (e) => {
      canvas.removeEventListener('mousemove', mouseMoveHandle, false);
    })
  }
</pre>

> 上述例子为一个简单的绘图APi，用户每次在canvas元素上按下鼠标键都会触发Mousedown事件的处理程序，而这也是用户想在鼠标的当前位置开始画线的时候，事件处理程序会创建一条新的路径并通过调用context.moveTo方法将虚拟的绘图笔移动到鼠标所在的位置，随后它将为mousemove添加事件监听器，这样，用户每次移动鼠标的时候，mouseMoveHandle函数都会被调用，他会绘制一条到当前的鼠标位置的直线，并将路径轮廓渲染到canvas上，最后，还有一个mouseup事件的处理程序，起会移除mousemove事件处理程序，这样当鼠标释放后，就不再会有线条绘制到canvas上了。
