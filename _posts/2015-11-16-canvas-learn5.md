---
layout: post
title:	canvas-learn-5
tags: [canvas]
---

<h1 style="text-align:center;">旋转</h1>

### 生成一个箭头

> 每次需要一个箭头的时候，只需要调用new Arrow()方法即可

<pre>
'use strict';

class Arrow {
  constructor() {
    this.x = 0;
    this.y = 1;
    this.color = '#ffff00';
    this.rotation = 0;
  }

  draw(context) {
    context.save();
    context.translate(this.x, this.y);
    context.rotate(this.rotation);
    context.lineWidth = 2;
    context.fillStyle = this.color;
    context.beginPath();
    context.moveTo(-50, -25);
    context.lineTo(0, -25);
    context.lineTo(0, -50);
    context.lineTo(50, 0);
    context.lineTo(0, 50);
    context.lineTo(0, 25);
    context.lineTo(-50, 25);
    context.lineTo(-50, -25);
    context.closePath();
    context.fill();
    context.stroke();
    context.restore();
  }
}
</pre>

### 获取鼠标的当前位置

> 当鼠标位置在element中发生变化的时候，下面的方法会返回当前鼠标位置的坐标值

<pre>
'use strict';
window.utils = {};

window.utils.captureMouse = function(element) {
  let mouse, body_scrollLeft, element_scrollLeft, body_scrollTop, element_scrollTop, offsetLeft, offsetTop;
  mouse = {x : 0, y: 0, event: null};
  body_scrollLeft = document.body.scrollLeft;
  element_scrollLeft = document.documentElement.scrollLeft;
  body_scrollTop = document.body.scrollTop;
  element_scrollTop = document.documentElement.scrollTop;
  offsetLeft = element.offsetLeft;
  offsetTop = element.offsetTop;

  element.addEventListener('mousemove', function(event) {
    let x, y;
    if (event.pageX || event.pageY) {
      x = event.pageX;
      y = event.pageY;
    } else {
      x = event.clientX + body_scrollLeft + element_scrollLeft;
      y = event.clientY + body_scrollTop + element_scrollTop;
    }

    x -= offsetLeft;
    y -= offsetTop;
    console.log(`${x}=============================${y}`);
    mouse.x = x;
    mouse.y = y;
  }, false);

  return mouse;
}  
</pre>

### 改变箭头的角度

> 通过captureMouse(canvas)方法获取到鼠标的坐标值，然后可以通过箭头对象的x与y属性获得它的坐标位置，通过这两个坐标的差值，就可以计算出鼠标和箭头组成的三角形的两边长度。此时，只需要通过Math.atan2(dy, dx)方法算出角度的大小并将其赋值给箭头对象的rotation属性，过程如下：

<pre>
  'use strict';
  let dx = mouse.x - arrow.x,
      dy = mouse.y - arrow.y;
  arrow.ratation = Math.atan2(dy, dx);
</pre>


### 最后实现动画

> 使用window.requestAnimationFrame方法在设定好的时间间隔内不断的清空canvas并绘制新的帧，代码如下：

<pre>
'use strict';
window.onload = () => {
  let canvas = document.querySelector('#canvas'),
      context = canvas.getContext('2d'),
      mouse = utils.captureMouse(canvas),
      arrow = new Arrow();

  arrow.x = canvas.width / 2;
  arrow.y = canvas.height / 2;

  (function drawFrame() {
    window.requestAnimationFrame(drawFrame, canvas);
    context.clearRect(0, 0, canvas.width, canvas.height);

    let dx = mouse.x - arrow.x,
        dy = mouse.y - arrow.y;

    arrow.rotation = Math.atan2(dy, dx);
    arrow.draw(context);
  })();
}  
</pre>
