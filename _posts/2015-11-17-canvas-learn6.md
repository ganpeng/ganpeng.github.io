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

> 