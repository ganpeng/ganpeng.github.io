---
layout: post
title:	canvas-learn-6
tags: [canvas]
---

<h1 style="text-align:center;">线性垂直运动</h1>

<pre>
	'use strict';

	window.onload = function() {
		let canvas, context, ball, angle, range, xSpeed, ySpeed;

		canvas = document.querySelector('#canvas');
		context = canvas.getContext('2d');
		ball = new Ball();
		angle = 0;
		range = 100;
		xSpeed = 0.5;
		ySpeed = 0.05;

		// ball.x = canvas.width / 2;
		ball.x = 0 + ball.radius;
		ball.y = canvas.height / 2;
		(function drawFrame() {
			window.requestAnimationFrame(drawFrame, canvas);
			context.clearRect(0, 0, canvas.width, canvas.height);

			ball.x += xSpeed; // 水平方向的速度变化
			ball.y = canvas.height / 2 + Math.sin(angle) * range; 
			angle += ySpeed; // ySpeed通过改变角度的大小，改变小球在y轴上的坐标
			ball.draw(context);
		})();
	};
</pre>