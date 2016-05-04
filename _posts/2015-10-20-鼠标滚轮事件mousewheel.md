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

### 注意事项

> 当鼠标滚轮事件的目标元素的父元素的高度过高，出现滚动条是，如果在目标元素是执行滚动操作的时候，会触发滚动事件的默认行为，所以此处应该阻止其滚动事件的默认行为；

> 可以使用 return false 来阻止默认行为，也可以使用 event.preventdefault()来阻止默认行为
> 他们两者之间的区别是，return false 只能阻止 obj.on事件名称 = eventHandle,这种形式的事件绑定；而通过addEventListener绑定的事件则需要通过event下面的preventDefault()来阻止默认行为

<pre>
    document.oncontextMenu = (e) => { // 鼠标右键菜单的事件
        return false;  // 因为是on+事件名称 = 处理函数 形式的事件绑定，所以可以使用return false来阻止默认事件的行为
    }

    document.addEventListener('contextmenu', (e) => {
        // return false; // 但是此时是使用了addEventListener的事件绑定，所以return false不能阻止事件的默认行为
        e.preventDefault(); // 只能使用这种方法 
    }, false); 
</pre>

#### 完整示例代码

<pre>
    'use strict';

    window.onload = () => {
        let obj = document.querySelector('#div'),   
            status = null; // 如果status为true，则为向上滚动，如果为false, 则为向下滚动

        // obj.addEventListener('mousewheel', mousewheelHandle, false);

        obj.onmousewheel = mousewheelHandle;

        if (obj.addEventListener) {
            obj.addEventListener('DOMMouseScroll', mousewheelHandle, false);
        }

        function mousewheelHandle(e) {
            let event = e || window.e;
            /*
                ie/chrome  event.wheelDelta  上 ： -3， 下 ： 3；

                firefox  event.detail 上 ： 1， 下 ： -1；
             */

            if (event.wheelDelta) {
                status = event.wheelDelta < 0 ? true : false;
            } else {
                status = event.detail > 0 ? true : false;
            }

            if(status) {
                this.style.height = this.offsetHeight - 1 + 'px';
            } else {
                this.style.height = this.offsetHeight + 1 + 'px';
            }

            if (event.preventDefault) {
                event.preventDefault();
            }
            return false;
        }

        // document.oncontextmenu = (e) => {
        //  return false;
        // }    

        document.addEventListener('contextmenu', (e) => {
            // return false;
            e.preventDefault();
        }, false);
    }   
</pre>