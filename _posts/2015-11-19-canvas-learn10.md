---
layout: post
title:	canvas-learn-10
tags: [javascript]
---

<h1 style="text-align:center;">使用绘图API产生的波</h1>

> 主要需要注意的地方就是：
> 在drawFrame函数中取消了对context.clearRect的调用，这样cavnas元素就不会在每一帧开始的时候擦除之前绘制的图像，使得每一帧的图像都会保留在canvas上

<pre>
  'use strict';

  window.onload = () => {


    let canvas, context, angle, range, centerY, xSpeed, ySpeed, xpos, ypos;
    canvas = document.querySelector('#canvas');
    context = canvas.getContext('2d');
    angle = 0;
    range = 50;
    centerY = canvas.height / 2;
    xSpeed = 1;
    ySpeed = 0.05;
    xpos = 0;
    ypos = centerY;

    context.lineWidth = 2;

    (function drawFrame() {
      window.requestAnimationFrame(drawFrame, canvas);
      // context.clearRect(0, 0, canvas.width, canvas.height);
      context.beginPath();
      context.moveTo(xpos, ypos);
      xpos += xSpeed;
      angle += ySpeed;
      ypos = centerY + Math.sin(angle) * range;
      context.lineTo(xpos, ypos);
      context.stroke();
    })();

  }
</pre>
