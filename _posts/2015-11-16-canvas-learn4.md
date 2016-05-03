---
layout: post
title:	canvas-learn-4
tags: [canvas]
---

<h1 style="text-align:center;">动画中的三角学基础</h1>

## 弧度和角度

> 一弧度越等于57.2958度， 一个完整的圆，或者说360度等于6.2832弧度，即约等于2pi
> 转换公式：

> * 弧度：radians = degrees * Math.PI / 180
* 角度： degrees = radians * 180 / Math.PI

> 注意：

> canvas元素是基于视频画面的坐标系，其中(0, 0)处在空间的左上角;

> canvas元素中，顺时针的角度才是正值，逆时针的角度是负值;

> 正弦： 一个角度的正弦表示与该角相对的直角边与斜边的比例，可以用Math.sin(angle)表示;

> 余弦： 余弦表示角的邻边与斜边的比率，可以用 Math.cos(angle)表示;

> 注意： 一个角的正弦值等一另一个角的余弦值，而这个角的余弦值又恰好等于另一个角的正弦值

> 正切： Math.tan(angle)，它表现了对边与邻边的关系;

> 反正弦： 反正弦是正弦的逆运算，即是输入一个比率，获得对应的角的弧度，可以使用Math.asin(ratio)表示;

> 反余弦： 反余弦是余弦的逆运算，可以用Math.acos(ratio)表示;

> 反正切： 反正切是正切的逆运算，输入角的对边与邻边的比率，通过计算反正切可以得到角的弧度。有两种表示方法：

> * Math.atan(ratio);
* Math.atan2(y, x); // x, y为点的x，y坐标;
