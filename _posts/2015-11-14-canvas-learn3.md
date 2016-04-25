---
layout: post
title:	canvas-learn-3
tags: [javascript]
---

<h1 style="text-align:center;">用户交互</h1>

### 事件与事件处理程序

> * 监听器
*  事件处理程序

> 监听器决定了一个元素是否因该响应某个事件，而事件处理程序则是当事件发生时将要调用的函数。监听函数如下：
<pre>
  element.addEventListener(type, handler, [, useCapture]);
</pre>
> 第一个参数是一个字符串，该字符串用于指定所要监听的事件的类型;

> 第二个参数则是元素接收到事件后要调用的事件处理程序;

> 第三个参数是可选的，该参数会影响到事件如何沿着DOM树向上传递;

> <p style="color:red;">注意:</p>
> <p style="color:green;">在监听器的内部实现中，触发事件的对象会维护一个列表，其中包含每个监听器对象。如果一个对象能够触发多种类型的事件，如mousedown,mouseup与mousemove，则它会为它可以触发的每一个事件类型维护一个监听器列表。每当其中的一个事件发生时，该对象就会遍历对应的列表并通知其中的每个对象什么时候事件发生了。</p>

> 取消事件的监听的方法：
> <pre>
  elelment.removeEventListener(type, handler, [, useCapture]);
</pre>

### 鼠标位置

> 每个鼠标事件有两个属性用于确定鼠标的当前位置：pageX和pageY，结合这两个属性以及canvas元素相对文件的偏移量，可以确定鼠标在canvas元素上的相对坐标。遗憾的是，并不是所有的浏览器都支持这两个属性，所以在这些情况下，可能要用到clientX和clientY。以下是获取鼠标位置的函数：
> <pre>
  function captureMouse(ele) {
  let mouser = {
  x : 0,
  y : 0
};
  ele.addEventListener('mousemove', (e) => {
  let x, y;
  if (e.pageX || e.pageY) {
  x = e.pageX;
  y = e.pageY;
} else {
  x = e.clientX + document.body.scrollLeft + document.docuemntElement.scrollLeft;
  y = e.clientY + document.body.scrollTop + document.documentElement.scrollTop;
}
  x -= ele.offsetLeft;
  y -= ele.offsetTop;
  mouse.x = x;
  mouse.y = y;
  }, false);
  return mouse;
}
<pre>

触摸事件

> 如下captureTouch函数确定第一个手指在元素上触摸的位置。不过由于可能出现没有手指触摸到屏幕的情况，因此为返回的对象添加了一个isPressed属性。同时，如果没有手指触摸到屏幕，x与y属性就会设置为null

> <pre>
  function captureTouch(ele) {
  let touch = {
  x : null,
  y : null,
  isPressed : false
};
  ele.addEventListener('touchstart', (e) => {
      touch.isPressed = true;
  }, false);
  ele.addEventListener('touchend', (e) => {
      touch.isPressed = false;
      touch.x = null;
      touch.y = null;
    }, false);
  ele.addEventListener('touchmove', (e) => {
    let x, y, touch_event = e.touches[0]; // first touch
    if (touch_event.pageX || touch_event.pageY) {
      x = touch_event.pageX;
      y = touch_event.pageY;
    } else {
      x = touch_event.clientX + document.body.scrollLeft + document.documentElement.scrollLeft;
      y = touch_event.clientY + document.body.scrollTop + document.documentElement.scrollTop;
    }
    x -= offsetLeft;
    y -= offsetTop;  
    touch.x = x;
    touch.y = y;
    }, false);
    return touch;
}
</pre>


### 键盘事件

>大多数情况下直接在网页上监听键盘事件而不管谁获得了焦点，为了做到这点，可以直接将一个键盘事件监听器绑定到全局的window对象上，如下实例：

> <pre>
  function onKeyboardEvent(e) {
    console.log(e.type);
}

window.addEventListener('keydown', onKeyboardEvent, false);
window.addEventlistener('keyup', onKeyboardEvent, false);
</pre>
