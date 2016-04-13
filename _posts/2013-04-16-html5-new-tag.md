---
layout: post
title:	html5新标签元素的用法总结 
tags: [html]
---

<!-- # html5新标签元素总结 -->

###SEMANTICS（新的语义标签）
####1. section
	<section> 标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
示例：	
	
	<section>
	  <h1>Forest elephants</h1>    
	  <p>In this section, we discuss the lesser known forest elephants. 
	    ... 代码摘自MDN ...
	  <section>
	    <h2>Habitat</h2>  
	    <p>Forest elephants do not live in trees but among them.
	        ...this subsection continues...
	  </section>
	</section>
	<section>
	  <h3>Mongolian gerbils</h3>
	  <p>In this section, we discuss the famous mongolian gerbils. 
	     ...this section continues...
	</section>
	
####2. article
	<article> 标签规定独立的自包含内容，一篇文章应有其自身的意义，应该有可能独立于站点的其余部分对其进行分发。
	<article> 元素的潜在来源：
		* 论坛帖子
		* 报纸文章
		* 博客条目
		* 用户评论
		
示例：

	<article>
  		<h1>Google Chrome</h1>
  		<p>Google Chrome is a free, open-source web browser developed by Google, released in 2008.p>
	</article>
	
####3. aside
	<aside> 标签定义其所处内容之外的内容,aside 的内容应该与附近的内容相关。
	<aside> 的内容可用作文章的侧栏。
	
示例：

	<p>Me and my family visited The Epcot center this summer.</p>
	<aside>
		<h4>Epcot Center</h4>
		The Epcot Center is a theme park in Disney World, Florida.
	</aside>	

####4. nav
	<nav> 标签定义导航链接的部分。
	如果文档中有“前后”按钮，则应该把它放到 <nav> 元素中。
		
示例：

	<nav>
	  <ul>
	    <li><a href="#">Home</a></li>
	    <li><a href="#">About</a></li>
	    <li><a href="#">Contact</a></li>
	  </ul>
	</nav>
	
####5. header
	<header> 标签定义文档的页眉（介绍信息）。	
	
示例：

	<header>
  		a logo
	</header>
	
####6. footer
	
	<footer> 标签定义文档或节的页脚。
	<footer> 元素应当含有其包含元素的信息
	页脚通常包含文档的作者、版权信息、使用条款链接、联系信息等等。
	您可以在一个文档中使用多个 <footer> 元素。
	<footer> 元素内的联系信息应该位于 <address> 标签中.

示例：
	
	<footer>
  		<p>Posted by: W3School</p>
  		<p>Contact information: <a href="mailto:someone@example.com">someone@example.com</a>.</p>
	</footer>

####7. hgroup
	<hgroup> 标签用于对网页或区段（section）的标题进行组合。
	请使用 <figcaption> 元素为元素组添加标题
	
示例：
	
	<hgroup>
  		<h1>Welcome to my WWF</h1>
  		<h2>For a living planet</h2>
	</hgroup>

	<p>The rest of the content...</p>
	
####8. command
	command 元素表示用户能够调用的命令。
	<command> 标签可以定义命令按钮，比如单选按钮、复选框或按钮。
	只有当 command 元素位于 menu 元素内时，该元素才是可见的。否则不会显示这个元素，但是可以用它规定键盘快捷	键。
	只有 Internet Explorer 9 （更早或更晚的版本都不支持）支持 <command> 标签。
	
示例：
	
	<command type="command" label="Save" icon="icons/save.png" onclick="save()">
	
####9. datalist
	<datalist> 标签定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值。
	datalist 及其选项不会被显示出来，它仅仅是合法的输入值列表。
	请使用 input 元素的 list 属性来绑定 datalist。
	所有主流浏览器都支持 <datalist> 标签，除了 Internet Explorer 和 Safari。
	
示例：
	
	<label>Choose a browser from this list:
		<input list="browsers" name="myBrowser" />
	</label>
	<datalist id="browsers">
			<option value="Chrome">
 			<option value="Firefox">
 			<option value="Internet Explorer">
 			<option value="Opera">
 			<option value="Safari">
 			<option value="Microsoft Edge">
	</datalist>
	
####10. details
	<details> 标签用于描述文档或文档某个部分的细节。
	与 <summary> 标签 配合使用可以为 details 定义标题。标题是可见的，用户点击标题时，会显示出 details。
	目前只有 Chrome 支持 <details> 标签。
	
示例：

	<details>
	  <summary>Some details</summary>
	  <p>More info about the details.</p>
	</details>

####11. embed
	<embed> 标签定义嵌入的内容，比如插件。
	
<table>
	<thead>
		<tr>
			<th>属性</th>
			<th>值</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>height</td>
			<td>pixels</td>
			<td>设置嵌入内容的高度。</td>
		</tr>
		<tr>
			<td>src</td>
			<td>url</td>
			<td>嵌入内容的 URL。</td>
		</tr>
		<tr>
			<td>type</td>
			<td>type</td>
			<td>定义嵌入内容的类型。</td>
		</tr>
		<tr>
			<td>width</td>
			<td>pixels</td>
			<td>设置嵌入内容的宽度。</td>
		</tr>
	</tbody>
</table>
	
示例：
	
	<embed type="video/quicktime" src="movie.mov" width="640" height="480">
	
####12. figcaption
	用作文档中插图的图像，带有一个标题
	<figcaption> 标签定义 figure 元素的标题（caption）。
	"figcaption" 元素应该被置于 "figure" 元素的第一个或最后一个子元素的位置。
	所有主流浏览器都支持 <figcaption> 标签。
	
示例1 ：
	
	<!-- Just a figure -->
	<figure>
	 <img src="https://developer.cdn.mozilla.net/media/img/mdn-logo-sm.png" alt="An awesome picture">
	</figure>
	<p></p>
	<!-- Figure with figcaption -->
	<figure>
	 <img src="https://developer.cdn.mozilla.net/media/img/mdn-logo-sm.png" alt="An awesome picture">	
	 <figcaption>Fig1. MDN Logo</figcaption>
	</figure>
	<p></p>
	
示例2 ：
	
	<figure>
	  <figcaption>Get browser details using navigator</figcaption>
	  <pre>
		function NavigatorExample() {
		  var txt;
		  txt = "Browser CodeName: " + navigator.appCodeName;
		  txt+= "Browser Name: " + navigator.appName;
		  txt+= "Browser Version: " + navigator.appVersion ;
		  txt+= "Cookies Enabled: " + navigator.cookieEnabled;
		  txt+= "Platform: " + navigator.platform;
		  txt+= "User-agent header: " + navigator.userAgent;
		}            
	  </pre>
	</figure>
如下是示例2的显示结果


<figure>
  <figcaption>Get browser details using navigator</figcaption>
  <pre>
	function NavigatorExample() {
	  var txt;
	  txt = "Browser CodeName: " + navigator.appCodeName;
	  txt+= "Browser Name: " + navigator.appName;
	  txt+= "Browser Version: " + navigator.appVersion ;
	  txt+= "Cookies Enabled: " + navigator.cookieEnabled;
	  txt+= "Platform: " + navigator.platform;
	  txt+= "User-agent header: " + navigator.userAgent;
	}            
  </pre>
</figure>

示例3： 
	
	<figure>
	  <figcaption><cite>Edsger Dijkstra :-</cite></figcaption>
	  <p>"If debugging is the process of removing software bugs, <br /> then programming must 		be the process of putting them in"</p>
	</figure>
	
示例4 ：

	<figure>
		 <p>
		  Depression is running through my head,<br>
		  These thoughts make me think of death,<br>
		  A darkness which blanks my mind,<br>
		  A walk through the graveyard, what can I find?....
		 </p>
		 <figcaption><cite>Depression</cite>. By: Darren Harris</figcaption>
	</figure>

####13. figure
	用作文档中插图的图像
	<figure> 标签规定独立的流内容（图像、图表、照片、代码等等）。
	figure 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响。
	请使用 <figcaption> 元素为 figure 添加标题（caption）。
	
示例请参见  **figcaption**

####14. keygen
	<keygen> 标签规定用于表单的密钥对生成器字段。
	当提交表单时，私钥存储在本地，公钥发送到服务器。
	所有主流浏览器都支持 <keygen> 标签，除了 Internet Explorer 和 Safari。
	
示例：
	
	<form action="demo_keygen.asp" method="get">
		Username: <input type="text" name="usr_name" />
		Encryption: <keygen name="security" />
		<input type="submit" />
	</form>
	
	<keygen name="name" challenge="challenge string" keytype="type" keyparams="pqg-params">
	
	已被web标准移除