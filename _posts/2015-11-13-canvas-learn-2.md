---
layout: post
title:	canvas-learn-2
tags: [canvas]
---

<h1 style="text-align:center;">动画的javascript基础</h1>

### 动画基础

> * 动画由帧组成，每一帧在表现运动的假象上有细微的差别;
* 逐帧动画包含每一帧的图像或图像的描述;
* 动态动画包含一副图片的起始描述以及后续每一帧图像的变化规则;

### 用代码实现动画

#### 动画循环
> 几乎所有的程序动画都会表现为某种形式的循环

> 获取初始化状态 => 渲染帧 => 应用规则 => 结束了吗? => 是则显示帧，否则渲染帧

> 以下是小球运动的规则：

<pre>
  let dx = mouse.x - ball.x,
      dy = mouse.y - ball.y,
      ax = dx * spring,
      ay = dy * spring;

  vx += ax;
  vy += ay;
  vx += gravity;
  vx *= friction;
  vy *= friction;

  ball.x += vx;
  ball.y += vy;

  ball.draw(context);
</pre>     

> 为了实现动画，需要为每一帧执行以下操作：
>
1 . 执行该帧所要调用到的代码;
>
2 . 将所有的对象绘制到canvas上;
>
3 . 重复这一过程渲染下一帧;

> 创建一个函数用于不断的更新对象的位置并将它绘制到canvas上，如下：

<pre>
  function drawFrame() {
    ball.x += 1;
    ball.draw(context);
  }

  window.setInterval(drawFrame, 1000 / 60);
</pre>

<h5 style="color:red;">注意： </h5>
> javascript定时器并不是为实现动画设计的。因为它无法达到毫秒级的精确度(每个浏览器的定时器的分辨率不同),所以无法依赖它实现高质量的动画。除此之外，通过第二个参数指定的间隔时间仅仅是在请求的那一时刻执行而已。如果同一时刻在浏览器的任务队列中有其他任务的话，动画代码的执行任务将不得不等待在哪里.

#### 使用requestAnimationFrame的动画循环

> 通过对requestAnimationFrame函数的链式调用实现动画的循环：

<pre>
  (function drawFrame() {
    window.requestAnimationFrame(drawFrame, canvas);
    })();
</pre>

> drawFrame函数中包含了每一帧将要执行的动画代码。该函数的第一行代码调用了window.requestAnimationFrame函数并将drawFrame函数自身的引用作为参数值传入。第二个可选参数是要绘制的canvas。当执行drawFrame函数时，window.requestAnimationFrame将drawFrame函数放入队列等待在下一个动画间隔中再次执行，而当它再次执行是又会重复这一过程，由于不断的请求该函数，因此就串联成了一个循环。

>  下面代码实现了对requestAnimationFrame函数的跨平台兼容：

<pre>
if (!window.requestAnimationFrame) {
  window.requestAnimationFrame = (window.webkitRequestAnimationFrame ||
   window.mozRequestAnimationFrame ||
   window.oRequestAnimationFrame ||
   window.msRequestAnimationFrame ||
   function (callback) {
     return window.setTimeout(callback, 1000 / 60);
     });
}
</pre>
