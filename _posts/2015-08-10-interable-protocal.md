<h1 style="text-align:center;">迭代协议</h1>

# 概述
> iterable protocal 是es6新增的一部分，不是新语法或一个新的内置对象，而是一种协议(protocol)。这种协议能被任何遵循某些约定的对象实现。

> 包含两类协议： 
>
* 可迭代协议
* 迭代器协议	

### 可迭代协议
> 可遍历（可迭代）协议允许 JavaScript 对象去定义或定制它们的迭代行为, 

> 例如（定义）在一个 for..of 结构中什么值可以被循环（得到）。一些内置类型都是内置的可遍历对象并且有默认的迭代行为, 比如 **Array** or **Map**, 另一些类型则不是 (比如Object) 。

> 为了变成可遍历对象， 一个对象必须实现 @@iterator 方法, 意思是这个对象（或者它原型链prototype chain上的某个对象）必须有一个名字是 **Symbol.iterator** 的属性

> 当一个对象需要被遍历的时候（比如开始用于一个for..of循环中），它的@@iterator方法被调用并且无参数，然后返回一个用于在遍历中获得值的迭代器。

### 迭代器协议
> 该迭代器协议定义了一个标准的方法来产生一个有限或无限序列的值。

> 当一个对象被认为是一个迭代器时，它实现了一个 next() 的方法并且拥有以下含义：
>
* done : 是否可迭代
* value : 迭代器返回的值

> 迭代器是转换自可遍历对象

<pre>
	var arr = [1, 2, 3];
	var arrEntries = arr.entries();
	arrEntries.toString();  // "[object Array Iterator]"
	arrEntries === arrEntries[Symbol.iterator]() // true
</pre>

#### 使用iteration protocols迭代协议的例子

> 字符串string是内置可遍历对象的例子

<pre>
	var str = 'hello';
	typeof str[Symbol.iterator] === 'function'; // true
</pre>
	
> string的默认迭代器返回字符串的每个字符

<pre>
	var strIterator = str[Symbol.iterator]();
	strIterator.toString() === '[object String Iterator]'; // true
	strIterator.next(); // Object {value: "h", done: false}
	strIterator.next(); // Object {value: "e", done: false}
	strIterator.next(); // Object {value: "l", done: false}
	strIterator.next(); // Object {value: "l", done: false}
	strIterator.next(); // Object {value: "o", done: false}
	strIterator.next(); // Object {value: undefined, done: true}
</pre>  

> 一些内置的语法结构, 比如扩展运算符[...str], 在幕后使用同样的iteration protocol:

<pre>
	var str = 'hello';
	[...str];  //  ["h", "e", "l", "l", "o"]
</pre>




















