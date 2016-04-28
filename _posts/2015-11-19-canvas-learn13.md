---
layout: post
title:	canvas-learn-13
tags: [javascript]
---

<h1 style="text-align:center;">两点之间的距离</h1>

### 原理

> 够固定里

> 给定两个点（x1, y1)和(x2, y2)，分别计算出x轴和y轴上的距离，取其平方，再求和，最后取平方根，代码如下：

<pre>
let dx = x2 - x1,
    dy = y2 - y1,
    dist = Math.sqrt(dx * dx + dy * dy);
</pre>

> 实例：

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        mouse = utils.captureMouse(canvas),
        rect = {
          x : canvas.width / 2,
          y : canvas.height / 2
        };

    (function drawFrame() {
      window.requestAnimationFrame(drawFrame, canvas);
      context.clearRect(0, 0, canvas.width, canvas.height);

      let dx = rect.x - mouse.x,
          dy = rect.y - mouse.y,
          dist = Math.sqrt(dx * dx + dy * dy);

      context.fillStyle = '#000';
      context.fillRect(rect.x -2, rect.y - 2, 4, 4);

      context.beginPath();
      context.moveTo(rect.x, rect.y);
      context.lineTo(mouse.x, mouse.y);
      context.closePath();
      context.stroke();

      console.log(`鼠标所在位置距离矩形的距离为： ${dist}`);
    })();
  }
</pre>
