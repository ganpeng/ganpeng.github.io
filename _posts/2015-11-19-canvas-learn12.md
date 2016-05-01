---
layout: post
title:	canvas-learn-12
tags: [canvas]
---

<h1 style="text-align:center;">椭圆运动</h1>

### 原理

> 为了获得一个椭圆，可以使用不同的半径用于计算x与y的坐标位置，让我们将其分别命名为radiusX和radiusY

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        centerX = canvas.width / 2,
        centerY = canvas.height / 2,
        ball = new Ball(),
        angle = 0,
        speed = 0.05,
        xpos = centerX,
        ypos = centerY,
        radiusX = 150,
        radiusY = 100;

        (function drawFrame() {
          window.requestAnimationFrame(drawFrame, canvas);
          context.clearRect(0, 0, canvas.width, canvas.height);
          ball.x = centerX + Math.cos(angle) * radiusX;
          ball.y = centerY + Math.sin(angle) * radiusY;
          angle += speed;

          ball.draw(context);
        })();
  }
</pre>
