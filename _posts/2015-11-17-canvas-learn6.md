---
layout: post
title:	canvas-learn-6
tags: [javascript]
---

<h1 style="text-align:center;">波</h1>

###  正弦波

> 0°的正弦值是0，90°或者π/2弧度的正弦值是1，180°或者π的正弦值又回到0，270°或者3π/2弧度的正弦值是-1，360°或者2π的正弦值又回到0,请看如下代码：
<pre>
	for (var angle = 0; angle < Math.PI * 2; angle += 0.1) {
		console.log(Math.sin(angle));
	}
</pre>

### 平滑的上下移动

> 如果某些物体需要平滑的上下或者左右移动，就可以使用Math.sin(angle);

> 通过不断的增加角的度数可以模拟实现从0变到1再变到-1最后回到0的效果，通过不断增加角的度数可以不断得到上下波动的波形，此时如果可以将正弦值乘以更大的数字，比如100， 就可以得到一系列从-100到100不断变化的值。

> 首先创建一个小球的类，可以通过new关键字实例化一个小球

<pre>
	'use strict';

	class Ball {
		constructor(radius, color) {
			this.x = 0;
			this.y = 0;
			this.radius = radius || 40;
			this.color = color || '#ff0000';	
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
			if (this.lineWidth > 0) {
				context.stroke();
			}
			context.restore();
		}
	}
</pre>

> 创建一个Ball类的实例，并将这个小球绘制到canvas上，随后通过drawFrame函数与window.requestAnimationFrame函数设置一个动画循环使得球体上下运动，代码如下：

<pre>
	'use strict';

	window.onload = function() {
		let canvas, context, ball, angle;

		canvas = document.querySelector('#canvas');
		context = canvas.getContext('2d');
		ball = new Ball();
		angle = 0;

		ball.x = canvas.width / 2;
		ball.y = canvas.height / 2;
		(function drawFrame() {
			window.requestAnimationFrame(drawFrame, canvas);
			context.clearRect(0, 0, canvas.width, canvas.height);

			ball.y = canvas.height / 2 + Math.sin(angle) * 100;
			angle += 0.1;
			ball.draw(context);
		})();
	};	
</pre>

> 首先初始化一个angle = 0, 然后在drawFrame函数中，将angle属性的正弦值乘以50， 则可以等到-50到50之间的一系列值，再将这一系列值加上canvas高度的一半，一次作为球体在canvas中的y轴坐标，并在循环中以0.1为步长不断增加angle属性的大小，这样就可以获得一个平滑的上下运动.
> 其中，如果将0.1改成其他的值，则会影响运动的速度，因为角度增加的快慢会影响到它的正弦值从1变到-1的速度。而改变50则会影响到球形运动范围的远近，其中canvas.height / 2决定了球形运动的中心点, 抽象出这些值，可以得到如下代码:

<pre>
	'use strict';

	window.onload = function() {
		let canvas, context, ball, angle, range, speed;

		canvas = document.querySelector('#canvas');
		context = canvas.getContext('2d');
		ball = new Ball();
		angle = 0;
		range = 100; // 影响动画的范围
		speed = 0.5; // 影响动画的速度

		ball.x = canvas.width / 2;
		ball.y = canvas.height / 2;
		(function drawFrame() {
			window.requestAnimationFrame(drawFrame, canvas);
			context.clearRect(0, 0, canvas.width, canvas.height);

			ball.y = canvas.height / 2 + Math.sin(angle) * range; 
			angle += speed;
			ball.draw(context);
		})();
	};	
</pre>

> 避免在动画中出现具体的数字