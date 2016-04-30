-n--
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

#### 创建多条曲线

> 方法一：如下window.onload函数中的第一个for循环创建一个包含9个点的数组，每个点都是一个拥有x,y属性的对象，他们随机的放置在canvas上，开始一条新的路径，把画笔移动到第一个点的位置。接下来的for循环从1开始以2为步长递增，绘制一条曲线经过点1到达2,然后经过点2到达点4,再经过点5到达点6,最后经过点7到达点8.循环在点8结束，而它恰好是最后一个点。至少包含三个点，而且点的个数必须为奇数

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        number = 10,
        points = [];
    for (let i = 0; i < number; i++) {
      let point = {
        x : Math.random() * canvas.width,
        y : Math.random() * canvas.height
      };

      points.push(point);
    }

    context.beginPath();
    context.moveTo(points[0].x, points[0].y);

    for (let i = 1; i < number; i += 2) {
      context.quadraticCurveTo(points[i].x, points[i].y, points[i + 1].x, points[i + 1].y);
      context.stroke();
    }

  }
</pre>

> 方法二：上述方法创建的线条不像是一条平滑的曲线，必须插入一些更多的点让它看上去更像曲线，方法如下：在每两个点之间，加入一个切好位于他们中间的新点，并使用他们作为每条曲线的起点和终点，而将原始点作为曲线的控制点，代码如下：

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        number = 10,
        points = [];
    for (let i = 0; i < number; i++) {
      let point = {
        x : Math.random() * canvas.width,
        y : Math.random() * canvas.height
      };

      points.push(point);
    }

    context.beginPath();
    context.moveTo(points[0].x, points[0].y);

    for (var i = 1; i < number - 2; i++) {
      let x = (points[i].x + points[i + 1].x) / 2,
          y = (points[i].y + points[i + 1].y) / 2;
      context.quadraticCurveTo(points[i].x, points[i].y, x, y);
      context.stroke();
    }

    context.quadraticCurveTo(points[i].x, points[i].y, points[i + 1].x, points[i + 1].y);
    context.stroke();
  }
</pre>

#### 闭合的多条曲线

<pre>
  'use strict';

  window.onload = () => {
  let canvas = document.querySelector('#canvas'),
      context = canvas.getContext('2d'),
      number = 10,
      ctrlPoint = {},
      ctrlPoint1 = {},
      points = [];
  for (let i = 0; i < number; i++) {
    let point = {
      x : Math.random() * canvas.width,
      y : Math.random() * canvas.height
    };

    points.push(point);
  }

  ctrlPoint1.x = (points[0].x + points[number - 1].x) / 2;
  ctrlPoint1.y = (points[0].y + points[number - 1].y) / 2;
  context.beginPath();
  context.moveTo(ctrlPoint1.x, ctrlPoint1.y);

  for (var i = 1; i < number - 2; i++) {
    ctrlPoint.x = (points[i].x + points[i + 1].x) / 2,
    ctrlPoint.y = (points[i].y + points[i + 1].y) / 2;
    context.quadraticCurveTo(points[i].x, points[i].y, ctrlPoint.x, ctrlPoint.y);
    context.stroke();
  }

  context.quadraticCurveTo(points[i].x, points[i].y, ctrlPoint1.x, ctrlPoint1.y);
  context.stroke();
  }
</pre>

#### 绘制一个圆形

> arc(x, y, radius, startAngle, endAngle, [, antiClockwise]) : 为连接到前一个点的直线路径添加一个弧度，该弧度将是以x,y作圆心，以radius为半径的一个圆的一部分，该部分的起始角度和终止角度分别由startAngle和endAngle指定。

<pre>
context.beginPath();
context.arc(100, 100, 50, 0, Math.PI * 2, true);
context.closePath();
context.stroke();
</pre>

### 渐变

> canvas支持的渐变方式：

> 线性渐变： context.createLinearGradient(x0, y0, x1, y1);

> 放射性渐变： context.createRadialGradient(x0, y0, r0, x1, y1, r1);

> 设置渐变颜色 ： gradient.Gradient.addColorStop(ratio, color);

> 实例1：
<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        pt1 = {
          x : 0,
          y : 0
        },
        pt2 = {
          x : 100,
          y : 100
        },
        gradient = context.createLinearGradient(pt1.x, pt1.y, pt2.x, pt2.y);


        gradient.addColorStop(0, '#ffffff');
        gradient.addColorStop(1, '#ff0000');

        context.fillStyle = gradient;
        context.fillRect(0, 0, 100, 100);
  }
</pre>

> 实例2：

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        c1 = {
          x : 150,
          y : 150,
          r : 0
        },
        c2 = {
          x : 150,
          y : 150,
          r : 50
        },
        gradient = context.createRadialGradient(c1.x, c1.y, c1.r, c2.x, c2.y, c2.r);


        gradient.addColorStop(0, '#ffffff');
        gradient.addColorStop(1, '#ff0000');

        context.fillStyle = gradient;
        context.fillRect(100, 100, 100, 100);
  }
</pre>

#### 加载并绘制图像

> context.drawImage方法将图片绘制到canvas元素上，该方法接收一个图片元素与canvas上的一个x, y坐标

> drawImage(image, dx, dy):在canvas的(dx, dy)坐标上绘制一张图片，(dx, dy)是图片左上角所在的位置;

> drawImage(image, dx, dy, dw, dh): 分别根据dw,dh的值设定图片的宽度和高度，并将其绘制在canvas上的(dx, dy)坐标;

> drawImage(image, sx, sy, sw, sh, dx, dy, dw, dh): 将图片裁剪到矩形区域(sx, sy, sw, sh)中，并缩放至(dh, dw), 再将其绘制到(dx, dy)坐标;

<pre>
  'use strict';

  window.onload = () => {
    let canvas = document.querySelector('#canvas'),
        context = canvas.getContext('2d'),
        img = new Image();

        img.onload = () => {
          context.drawImage(img, 0, 0);
        };

        img.src = 'http://www.sanguosha.com/images/23/123/1107/26/73/9779_10133273.PNG';
  }
</pre>
