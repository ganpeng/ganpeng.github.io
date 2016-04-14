---
layout: post
title:	flex 布局用法总结 
tags: [css]
---



<h2 style="text-align:center;">FLEX 弹性盒模型</h2>



## 弹性盒模型的概念

    CSS3 弹性盒（ Flexible Box 或 flexbox），是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。
    弹性盒中的子元素通过在各个方向放置就可以以弹性的尺寸适应父元素的显示区域。由于子元素的显示顺序和它们在代码中 的顺序是独立的，通过使用弹性盒，定位子元素变得更加简单，复杂的布局也能够使用更清晰的代码更简单的实现。独立显示被设定成只针对可见元素，而不是基于代码的声明和导航顺序。
	弹性盒布局的定义中，它可以自动调整子元素的高和宽，来很好的填充任何显示设备中的可用显示空间，收缩内容防止内容溢出。
	不同于块级元素基于垂直方向布局以及行内元素基于水平方向布局，弹性盒布局的算法是方向无关的。 虽然块级元素布局在页面中工作良好，但是其定义不足以支持那种需要根据用户代理从竖直切换成水平等变化而进行方向切换、大小调整、拉伸、收缩的引用组件。不同于将要出现的网格布局针对目标为大比例布局，弹性盒布局更适用于应用组件和小比例布局。这两种都是CSS工作组为了能与不同用户代理、不同书写模式和其他弹性需要进行协作而做出的努力。
	
	
	
## 弹性盒模型布局名词解释
	
![flex](https://developer.mozilla.org/files/3739/flex_terms.png)



#### 1.弹性容器
	弹性子元素的父元素。 通过设置display 属性的值为flex 或 inline-flex将其定义为弹性容器。
	
		* display: flex 值表示弹性容器为块级
		* display: inline-flex 值表示弹性容器为原子行级元素
	
#### 2.弹性子元素
	弹性容器的每一个子元素变为一个弹性子元素。弹性容器直接包含的文本变为匿名的弹性子元素。
	
#### 3.轴
	每个弹性盒布局以两个轴来排列。弹性子元素沿着主轴依次相互排列。侧轴垂直于主轴。
	
		* 属性 flex-direction 定义主轴方向。
		* 属性 justify-content 定义了弹性子元素如何在当前线上沿着主轴排列。
		* 属性 align-items 定义了弹性子元素如何在当前线上沿着侧轴排列。
		* 属性 align-self 覆盖父元素的align-items属性，定义了单独的弹性子元素如何沿着侧轴排列。
		
#### 4.方向
	弹性容器的主轴开始、主轴结束和侧轴开始、侧轴结束边缘代表了弹性子元素排列的起始和结束位置。它们具体取决于由writing-mode（从左到右、从右到左等等）属性建立的向量中的主轴和侧轴位置。
	
		* 属性 order 将元素依次分组，并决定谁先出现。
		* 属性 flex-flow 是属性 flex-direction 和 flex-wrap 的简写，用于排列弹性子元素。

#### 5.行
	弹性子元素根据 flex-wrap 属性控制的侧轴方向（在这个方向上可以建立垂直的新线），既可以是一行也可以是多行排	列。

#### 6.尺寸
	弹性子元素宽高可相应地等价于主尺寸和侧尺寸，它们都分别取决于弹性容器的主轴和侧轴。
	
		*  min-height 和 min-width 属性的初始值为新增关键字 auto
		* 属性 flex 是 flex-basis，flex-grow 和 flex-shrink 的缩写，代表弹性子元素的伸缩性。
		

## 注意事项
	1： 包含在弹性容器内的文本自动成为匿名的弹性子元素。然而，只包含空白的弹性子元素不会被渲染，就好像它被设定为display:none 一样。
	
	2： 弹性容器的绝对定位的子元素会被定位，因此其静态位置会根据它们的弹性容器的主起始内容盒的角落上开始。
	
	3：相邻的弹性子元素不会发生外边距合并。使用auto 的外边距会在垂直和水平方向上带来额外的空间，这种性质可用于		对齐或分隔临近的弹性子元素。
	
	4： 为了保证弹性子元素有一个合理的默认最小尺寸，使用 min-width:auto 与 min-height:auto。对于弹性子元素， auto 属性计算其最小的宽高不小于其内容的尺寸，保证在渲染时其大小足够容纳内容。
	
	5： 不影响弹性盒子的属性 
			
			*  多列模块 中的column-*属性对弹性子元素无效。
			*  float 和 clear 对弹性子元素无效。使用 float 会导致 display 属性计算为 block.
			*  vertical-align 对弹性子元素的对齐无效。
			
### 例子1
	
	<!DOCTYPE html>
	<html lang="en">
	  <head>
	    <style>
	
	   .flex
	   {
	      /* basic styling */
	      width: 350px;
	      height: 200px;
	      border: 1px solid #555;
	      font: 14px Arial;
	
	      /* flexbox setup */
	      display: -webkit-flex;
	      -webkit-flex-direction: row;
	
	      display: flex;
	      flex-direction: row;
	   }
	
	   .flex > div
	   {
	      -webkit-flex: 1 1 auto;
	      flex: 1 1 auto;
	
	      width: 30px; /* To make the transition work nicely.  (Transitions to/from
	                      "width:auto" are buggy in Gecko and Webkit, at least.
	                      See http://bugzil.la/731886 for more info.) */
	
	      -webkit-transition: width 0.7s ease-out;
	      transition: width 0.7s ease-out;
	   }
	
	   /* colors */
	   .flex > div:nth-child(1){ background : #009246; }
	   .flex > div:nth-child(2){ background : #F1F2F1; }
	   .flex > div:nth-child(3){ background : #CE2B37; }
	
	   .flex > div:hover
	   {
	        width: 200px;
	   }
	   
	   </style>
	    
	 </head>
	 <body>
	  <p>Flexbox nuovo</p>
	  <div class="flex">
	    <div>uno</div>
	    <div>due</div>
	    <div>tre</div>
	  </div>
	 </body>
	</html>
	
效果
	
<div style="width:350px;height:100px;border:1px solid #555;font:14px Arial;display:flex;display:-webkit-flex;">
	<div style="flex:1 1 auto;-webkit-flex:1 1 auto; width:30px; -webkit-transition:width 0.7s ease-out;transition:width 0.7s ease-out;background:#F1F2F1;"></div>
	<div style="flex:1 1 auto;-webkit-flex:1 1 auto; width:30px; -webkit-transition:width 0.7s ease-out;transition:width 0.7s ease-out;background:#009246;"></div>
	<div style="flex:1 1 auto;-webkit-flex:1 1 auto; width:30px; -webkit-transition:width 0.7s ease-out;transition:width 0.7s ease-out;background:#CE2B37;"></div>
</div>	


### 例子2

	<!DOCTYPE html>
	<html lang="en">
	  <head>
	    <style>
	
	  body {
	   font: 24px Helvetica;
	   background: #999999;
	  }
	
	  #main {
	   min-height: 800px;
	   margin: 0px;
	   padding: 0px;
	   display: -webkit-flex;
	   display:         flex;
	   -webkit-flex-flow: row;
	           flex-flow: row;
	   }
	 
	  #main > article {
	   margin: 4px;
	   padding: 5px;
	   border: 1px solid #cccc33;
	   border-radius: 7pt;
	   background: #dddd88;
	   -webkit-flex: 3 1 60%;
	           flex: 3 1 60%;
	   -webkit-order: 2;
	           order: 2;
	   }
	  
	  #main > nav {
	   margin: 4px;
	   padding: 5px;
	   border: 1px solid #8888bb;
	   border-radius: 7pt;
	   background: #ccccff;
	   -webkit-flex: 1 6 20%;
	           flex: 1 6 20%;
	   -webkit-order: 1;
	           order: 1;
	   }
	  
	  #main > aside {
	   margin: 4px;
	   padding: 5px;
	   border: 1px solid #8888bb;
	   border-radius: 7pt;
	   background: #ccccff;
	   -webkit-flex: 1 6 20%;
	           flex: 1 6 20%;
	   -webkit-order: 3;
	           order: 3;
	   }
	 
	  header, footer {
	   display: block;
	   margin: 4px;
	   padding: 5px;
	   min-height: 100px;
	   border: 1px solid #eebb55;
	   border-radius: 7pt;
	   background: #ffeebb;
	   }
	 
	  /* Too narrow to support three columns */
	  @media all and (max-width: 640px) {
	  
	   #main, #page {
	    -webkit-flex-flow: column;
	            flex-flow: column;
	   }
	
	   #main > article, #main > nav, #main > aside {
	    /* Return them to document order */
	    -webkit-order: 0;
	            order: 0;
	   }
	  
	   #main > nav, #main > aside, header, footer {
	    min-height: 50px;
	    max-height: 50px;
	   }
	  }
	
	 </style>
	  </head>
	  <body>
	 <header>header</header>
	 <div id='main'>
	    <article>article</article>
	    <nav>nav</nav>
	    <aside>aside</aside>
	 </div>
	 <footer>footer</footer>
	  </body>
	</html>
效果

 <header style="display:block;margin:4px;padding:5px;min-height:100px;border: 1px solid #eebb55;border-radius: 7pt;background: #ffeebb;">header</header>
 <div style="min-height:400px;margin:0px;padding:0px;display:-webkit-flex; display:flex;-webkit-flex-flow:row;flex-flow:row;"> 
 <article style="margin:4px;padding:5px;border:1px solid #cccc33;border-radius:7pt;background:#dddd88;-webkit-flex: 3 1 60%;flex: 3 1 60%;-webkit-order: 2;order: 2;">article</article>
    <nav style="margin: 4px;padding: 5px;border: 1px solid #8888bb;border-radius: 7pt;background: #ccccff;-webkit-flex: 1 6 20%;flex: 1 6 20%;-webkit-order: 1;order: 1;">nav</nav>
    <aside style="margin:4px;padding:5px;border:1px solid #8888bb;border-radius: 7pt;background:#ccccff;-webkit-flex:1 6 20%;flex:1 6 20%;-webkit-order:3;order:3;">aside</aside>
 </div>
 <footer style="display:block;margin:4px;padding:5px;min-height:100px;border: 1px solid #eebb55;border-radius: 7pt;background: #ffeebb;">footer</footer>
	
	
	
## 属性介绍

### 1: align-content
	align-content 属性定义弹性容器的侧轴方向上有额外空间是，如何排布每一行，当弹性容器只有一行时无作用
	
	语法：(默认stretch)
		
		align-content: flex-start| flex-end | center | space-between | space-around | stretch| inherit
		
	*  flex-start : 所有行从垂直起点开始填充，第一行的垂直起点边和容器的垂直轴起点边对齐。接下来的每一行紧跟前一行
	
	*  flex-end : 所有行从垂直轴终点开始填充。第一行的垂直轴终点边和容器的垂直轴终点边对齐。接下来的每一行紧跟前一行。
	
	*  center : 所有行朝向容器的中心填充。每行互相紧挨，相对于容器居中对齐。容器的垂直轴起点边和第一行的距离相等于容器的垂直轴终点边和最后一行的距离。
	
	*  space-between : 所有行在容器中平均分布。相邻两行间距相等。容器的垂直轴起点边和终点边分别与第一行和最后一行的边对齐。

	*  space-around : 所有行在容器中平均分布，相邻两行间距相等。容器的垂直轴起点边和终点边分别与第一行和最后一行的距离是相邻两行间距的一半。
	
	*  stretch : 拉伸所有行来填满剩余空间。剩余空间平均的分配给每一行
	
	
	
### 2: align-items


### 3: justify-content

### 示例

	/*
	* css
	*/
	#container > div {
	  display: flex;
	  font-family: "Courier New", "Lucida Console", monospace;
	}
	
	#container > div > div {
	  width: 50px;
	  height: 50px;
	  background: linear-gradient(-45deg, #788cff, #b4c8ff);
	}
	
	#flex-start {
	  justify-content: flex-start;
	}
	
	#center {
	  justify-content: center;
	}
	
	#flex-end {
	  justify-content: flex-end;
	}
	
	#space-between {
	  justify-content: space-between;
	}
	
	#space-around {
	  justify-content: space-around;
	}

	<!-- html -->
	
	
	<div id="container">
	  <p>justify-content: flex-start</p>
	  <div id="flex-start">
	    <div></div>
	    <div></div>
	    <div></div>
	  </div>
	
	  <p>justify-content: flex-end</p>
	  <div id="flex-end">
	    <div></div>
	    <div></div>
	    <div></div>
	  </div>
	
	  <p>justify-content: center</p>
	  <div id="center">
	    <div></div>
	    <div></div>
	    <div></div>
	  </div>
	
	  <p>justify-content: space-between</p>
	  <div id="space-between">
	    <div></div>
	    <div></div>
	    <div></div>
	  </div>
	
	  <p>justify-content: space-around</p>
	  <div id="space-around">
	    <div></div>
	    <div></div>
	    <div></div>
	  </div>
	</div>

效果

<div style='font-family: "Courier New", "Lucida Console", monospace;'>
 <p>justify-content: flex-start</p>
  <div id="flex-start" style="display:flex;justify-content: flex-start;">
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
  </div>



  <p>justify-content: flex-end</p>
  <div id="flex-end" style="display:flex;justify-content: flex-end;">
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
  </div>

  <p>justify-content: center</p>
  <div id="center" style="display:flex;justify-content: center;"> 
 	 <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
  </div>

  <p>justify-content: space-between</p>
  <div id="space-between" style="display:flex;justify-content: space-between;">
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
  </div>

  <p>justify-content: space-around</p>
  <div id="space-around" style="display:flex;justify-content: space-around;">
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
    <div style="  width: 50px; height: 50px; background: linear-gradient(-45deg, #788cff, #b4c8ff);"></div>
  </div>
</div>	


### 4: flex

	flex 属性是一个简写属性，它具有定义一个可伸缩项目的能力。flex元素可以根据他们的flex-grow 因子拉伸以填充可用空间，或根据他们的 flex-shrink 因子收缩以防止溢出。
	
	/* 0 0 auto */
	flex: none;
	
	/* 单值，没有单位的数字，是flex-grow */
	flex: 2;
	
	/* 单值，有单位的，宽、高，是flex-basis */
	flex: 10em;
	flex: 30px;
	flex: auto;
	flex: content;
	
	/* 两个值：flex-grow | flex-basis */
	flex: 1 30px;
	
	/* 两个值：flex-grow | flex-shrink */
	flex: 2 2;
	
	/* 三个值：flex-grow | flex-shrink | flex-basis */
	flex: 2 2 10%;
	
	/* 全局值 */
	flex: inherit;
	flex: initial;
	flex: unset;


示例： 

	// css
	#flex-container {
		display: -webkit-flex;
		display: flex;
		-webkit-flex-direction: row;
		flex-direction: row;
	}
	
	#flex-container > .flex-item {
		-webkit-flex: auto;
		flex: auto;
	}
	
	#flex-container > .raw-item {
		width: 5rem;
	}
	
	// html
	
	<div id="flex-container">
	    <div class="flex-item" id="flex">Flex box (click to toggle raw box)</div>
	    <div class="raw-item" id="raw">Raw box</div>
	</div>
	
效果

<div style="height:5rem;border:1px solid red;display:flex;display:-webkit-flex;">
    <div style="flex:auto;-webkit-flex:auto;border:1px solid pink;">Flex box (click to toggle raw box)</div>
    <div style="width:5rem;">Raw box</div>
</div>


### 5： flex-basis
	flex-basis 指定了flex item在主轴方向上的初始大小。如果不使用box-sizing来改变盒模型的话，那么这个属性就决定了flex item的内容盒（content-box）的宽或者高（取决于主轴的方向）的尺寸大小。
	
	语法：
	
	flex-basis: 10em      /* <'width'> */
	flex-basis: 3px       /* <'width'> */
	flex-basis: auto      /* <'width'> */
	flex-basis: content
	
	flex-basis: inherit
	
	<'width'>
	width值可以是一个数字后面跟着绝对单位例如px,mm,pt;该值也可以是一个百分数，那么这个百分数就是相对于其父弹性盒容器的宽或者高（取决于主轴方向）。负值是不被允许的。
	
示例：

	element { 
	  flex-basis: 18em;
	}

### 6： flex-flow
	flex-flow是一个简写的css属性，它由flex-direction(伸缩方向) 和 flex-wrap(是否强制换行)组成
	
示例：

	element { 
	  flex-flow: column-reverse wrap;            
	}
### 7： flex-grow
	flex-grow CSS属性定义弹性盒子项（flex item）的拉伸因子。

示例： 

	element { 
	  flex-grow: 3;
	}
	
### 8: flex-shrink
	flex-shrink 属性指定了flex item的收缩规则。
	
示例： 
	
	element { 
	  flex-shrink: 3;
	}
	
### 9： flex-wrap
	语法：
	flex-wrap: nowrap;
	flex-wrap: wrap;
	flex-wrap: wrap-reverse;
	
	/* Global values */
	flex-wrap: inherit;
	flex-wrap: initial;
	flex-wrap: unset;
	
	
示例：

	element {
	  flex-wrap: nowrap;
	}
		
### 10 ： order
	// html
	<!DOCTYPE html>
	<header>…</header>
	<div id='main'>
	   <article>…</article>
	   <nav>…</nav>
	   <aside>…</aside>
	</div>
	<footer>…</footer>
	
	//  css
	
	#main { display: flex; }
	#main > article { flex:1;         order: 2; }
	#main > nav     { width: 200px;   order: 1; }
	#main > aside   { width: 200px;   order: 3; }