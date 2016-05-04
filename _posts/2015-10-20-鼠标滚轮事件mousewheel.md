---
layout: post
title: 鼠标滚轮事件mousewheel 
tags: [javascript]
---

<h1 style="text-align:center;">鼠标滚轮事件mousewheel</h1>

###  兼容性

> ie/chrome ： mousewheel; // ie和chrome写鼠标滚轮事件是mousewheel;

> firefox ：DOMMouseScroll; // 而在firefox下鼠标滚轮事件是DOMMouseScroll, 该事件只能用addEventListener进行事件绑定；因为IE9以下不支持addEventListener,此处应该做一个特性侦测

<pre>
    'use strict';

    window.onload = () => {
        let obj = document.querySelector('#div');   

        // obj.addEventListener('mousewheel', mousewheelHandle, false);
        obj.onmousewheel = mousewheelHandle; // 此处为了兼容低版本的IE，使用onmousewheel事件

        if (obj.addEventListener) {
            obj.addEventListener('DOMMouseScroll', mousewheelHandle, false);
        }

        function mousewheelHandle(e) {
            alert(1);
        }
    }       
</pre>

### 鼠标滚轮事件的事件对象 

> ie/chrome : event.wheelDelta //  当向上滚动的时候，值为-3，向下滚动的时候值为3

> firefox : event.detail // 当向上滚动的时候，值为1，向下滚动的时候值为-1

> 兼容性处理如下:

<pre>
    'use strict';
    let status = null // 当status为true时表示向上滚动，当status值为false时表示向下滚动

    if (event.wheelDelta) {
        status = event.wheelDelta < 0 ? true : false;
    } else {
        status = event.detail > 0 ? true : false;
    }

</pre>

### 滚轮滚动处理

> 通过上述的处理，已经解决了各浏览器中的兼容性问题,现在只需要通过判断status的值，就能执行向上和向下滚动的处理函数了

if (status) {
    // 此处为向上滚动时要执行的处理
} else {
    // 此处为向下滚动时要执行的处理
}
