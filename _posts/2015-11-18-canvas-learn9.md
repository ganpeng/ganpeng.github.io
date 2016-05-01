---
layout: post
title:	canvas-learn-9
tags: [canvas]
---

<h1 style="text-align:center;">使用两个角产生正弦波</h1>

> 可以使用两个角，为它们设置不同的中心点和速度，然后将其中一个角的正弦波用于某个属性，再将另一个角的正弦波用于另一个属性

> 如下的例子，使用一个角的正弦波用于影响球形的x轴坐标，另一个用于改变球形的y坐标

<pre>
	'use strict';

	window.onload = function() {
		let canvas, context, ball, angleX, angleY, range, xSpeed, ySpeed, centerX, centerY;

		canvas = document.querySelector('#canvas');
		context = canvas.getContext('2d');
		ball = new Ball();
		angleX = 0;
		angleY = 0;
		centerX = canvas.width / 2;
		centerY = canvas.height / 2;
		range = 100;
		xSpeed = 0.05;
		ySpeed = 0.11

		ball.x = canvas.width / 2;
		ball.y = canvas.height / 2;
		(function drawFrame() {
			window.requestAnimationFrame(drawFrame, canvas);
			context.clearRect(0, 0, canvas.width, canvas.height);

			ball.x = centerX + Math.sin(angleX) * range; 
			ball.y = centerY + Math.sin(angleY) * range; 
			angleX += xSpeed;
			angleY += ySpeed;
			ball.draw(context);
		})();
	};	
</pre>