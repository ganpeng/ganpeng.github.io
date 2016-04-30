---
layout: post
title:  canvas-learn-15
tags: [javascript]
---

<h1 style="text-align:center;">使用quadraticCurveTo绘制曲线</h1>

### 简介

> context.quadraticCurveTo方法，通过一个控制点实现两点之间的曲线连接，context.quadraticCurveTo(cpx, cpy, x, y)该方法接收两个点参数，第一个点是控制点，用于影响曲线的形状，第二个点是曲线的终点。该形状由一个名为二次贝塞尔曲线的标准算法决定。

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        mouse = utils.captureMouse(canvas),
        x0 = 100,
        y0 = 200,
        x2 = 300,
        y2 = 200;


    canvas.addEventListener('mousemove', (e) => {
      context.clearRect(0, 0, canvas.width, canvas.height);

      let x1 = mouse.x,
          y1 = mouse.y;

      context.beginPath();
      context.moveTo(x0, y0);
      context.quadraticCurveTo(x1, y1, x2, y2);
      context.stroke();
    })
  }
</pre>

#### 穿过控制点的曲线

> 将目标点的坐标乘以2再减去起点和终点的坐标的平均值

> x1 = xt * 2 - (x0 + x2) / 2;

> y1 = yt * 2 - (y0 + y2) / 2;

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        mouse = utils.captureMouse(canvas),
        x0 = 100,
        y0 = 200,
        x2 = 300,
        y2 = 200;


    canvas.addEventListener('mousemove', (e) => {
      context.clearRect(0, 0, canvas.width, canvas.height);

      // let x1 = mouse.x,
      //     y1 = mouse.y;

      let x1 = mouse.x * 2 - (x0 + x2) / 2,
          y1 = mouse.y * 2 - (y0 + y2) / 2;

      context.beginPath();
      context.moveTo(x0, y0);
      context.quadraticCurveTo(x1, y1, x2, y2);
      context.stroke();
    })
  }
</pre>
