---
layout: post
title:	canvas-learn-8
tags: [javascript]
---

<h1 style="text-align:center;">脉冲运动</h1>

> 正弦值不仅仅可以用来改变对象的坐标，还可以用来改变对象的其他属性，可以使用正弦值改变对象的比例(scale)属性，来产生脉冲效果:

<pre>
	'use strict';

	window.onload = function() {
		let canvas, context, ball, angle, range, speed, centerScale;

		canvas = document.querySelector('#canvas');
		context = canvas.getContext('2d');
		ball = new Ball();
		angle = 0;
		centerScale = 1;
		range = 0.8;
		speed = 0.05;

		ball.x = canvas.width / 2;
		ball.y = canvas.height / 2;
		(function drawFrame() {
			window.requestAnimationFrame(drawFrame, canvas);
			context.clearRect(0, 0, canvas.width, canvas.height);

			ball.scaleX = centerScale + Math.sin(angle) * range; 
			ball.scaleY = centerScale + Math.sin(angle) * range; 
			angle += speed;
			ball.draw(context);
		})();
	};
</pre>

> <p style="color:red;">注意：</p>

> 正弦波还能改变其他的属性哦...
