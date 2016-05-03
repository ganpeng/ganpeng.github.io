---
layout: post
title:	canvas-learn-11
tags: [canvas]
---

<h1 style="text-align:center;">圆与椭圆</h1>

### 余弦运动

> 余弦运动中，0弧度的余弦值是1,在角的弧度变成2PI（即360度）的过程中，对应的余弦值依次变为0,-1,0,最终又变回1。这里的波形本质上与正弦波的波形是一样的，只是在x轴上产生了一些偏移而已。

#### 圆周运动

> 当余弦配合正弦使用时会获得一个更常用的并且更有价值的功能，让物体做圆周运动;

> 当从侧面观察物体的圆周运动时，你会发现物体实际是在做上下运动。上下运动的中心点是圆心所在的位置，而上下运动的范围正好是圆的半径。物体在运动中所处的位置为物体所处角度的正弦值与圆的半径的乘积;再想象从圆的底部进行观察，会发现物体在做前后运动;

<pre>
  'use strict';

  window.onload = () => {
  let canvas = document.querySelector('#canvas'),
      context = canvas.getContext('2d'),
      centerX = canvas.width / 2,
      centerY = canvas.height / 2,
      angle = 0,
      speed = 0.05,
      xpos = centerX,
      ypos = centerY,
      radius = 50;

      (function drawFrame() {
        window.requestAnimationFrame(drawFrame, canvas);
        context.beginPath();
        context.moveTo(xpos, ypos);

        angle += speed;
        xpos = centerX + Math.cos(angle) * radius;
        ypos = centerY + Math.sin(angle) * radius;

        context.lineTo(xpos, ypos);
        context.stroke();
      })();
  }
</pre>

> 以上代码使用余弦函数获得x坐标的大小，又通过正弦函数取得y坐标的大小，所以： 当我们从事动画编程的时候，每当我们谈到x时候，应该立即想到余弦， 而当我们谈到y时候，就应该立即想到正弦。

> 小球运动：

<pre>
  class Ball {
    constructor(radius, color) {
      this.x = 0;
      this.y = 0;
      this.radius = radius || 40;
      this.color = color || 'red';
      this.rotation = 0;
      this.scaleX = 1;
      this.scaleY = 1;
      this.lineWidth = 1;
    }

    draw(context) {
      context.save();
      context.translate(this.x, this.y);
      context.rotate(this.rotation);
      context.scale(this.scaleX, this.scaleY);
      context.lineWidth = this.lineWidth;
      context.fillStyle = this.color;
      context.beginPath();
      context.arc(0, 0, this.radius, 0, (Math.PI * 2), true);
      context.closePath();
      context.fill();
      if(this.lineWidth > 0) {
        context.stroke();
      }
      context.restore();
    }
  }
</pre>

> canvas渲染代码：

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
        radius = 150;

        (function drawFrame() {
          window.requestAnimationFrame(drawFrame, canvas);
          context.clearRect(0, 0, canvas.width, canvas.height);
          ball.x = centerX + Math.cos(angle) * radius;
          ball.y = centerY + Math.sin(angle) * radius;
          angle += speed;

          ball.draw(context);
        })();
  }
</pre>
