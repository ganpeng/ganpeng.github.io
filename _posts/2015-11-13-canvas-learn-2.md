---
layout: post
title:	canvas-learn-2
tags: [javascript]
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
