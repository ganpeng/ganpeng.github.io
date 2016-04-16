---
layout: post
title:	koa框架学习 
tags: [nodeJS]
---

<h1 style="text-align:center">Koa example</h1>

### 404 Handle

> 请求失败之后返回的页面

	'use strict'

	let koa = require('koa');
	
	let app = koa();
	
	app.use(function* (next) {
		yield next;
		if (this.status !== 404) {
			return 
		} 
	
		switch(this.accepts('html', 'json')) {
			case 'html' :
				this.type = 'html';
				this.body = '<p>Page Not Found</p>';
				break;
			case 'json' :
				this.body = {
					message : 'Page Not Found'
				};
				break;
			default :
				this.type = 'text';
				this.body = 'Page Not Found';
		}
	})
	
	
	app.listen(5000);
	
### koa-basic-auth
> 基本的用户访问认证

	'use strict'
	
	let koa = require('koa');
	
	let auth  = require('koa-basic-auth');
	
	let app = koa();
	
	app.use(function* (next){
	  try {
	    yield next;
	  } catch (err) {
	    if (401 == err.status) {
	      this.status = 401;
	      this.body = 'cant haz that';
	    } else {
	      throw err;
	    }
	  }
	});
	
	// require auth
	
	app.use(auth({ name: 'tj', pass: 'tobi' }));
	
	// secret response
	
	app.use(function* (){
	  this.body = 'secret';
	});
	
	app.listen(5000);
	
### co-body
> 基于co-body中间件的请求体解析实现



	'use strict'
	
	let koa = require('koa');
	
	let parse = require('co-body');
	
	let app = koa();
	
	app.use(function* (next) {
		if (this.method !== 'POST') {
			return yield next;
		}
	
		let body = yield parse(this, { limit : '1kb'});
		if (!body.name) {
			throw new Erorr(400, 'name required');
		}
		this.body = {
			name : body.name.toUpperCase()
		};
		console.log(this.body);
	})
	
	app.listen(5000);
	
### koa-body
> 基于koa-body中间件的请求体解析
	
	'use strict'
	
	let koa = require('koa');
	
	let koaBody = require('koa-body');
	
	let app = koa();
	
	app.use(koaBody({formidable:{uploadDir: __dirname + 'upload'}}));
	
	app.use(function* (next) {
		yield next;
		
		if (this.request.method === 'POST') {
			console.log(this.request.body);
			this.body = JSON.stringify(this.request.body);
		}
	})
	
	app.listen(5000);


### koa-compose
> 一个app.use()只能接受一个generator函数，要想将多个generator函数串联成一个，可以使用compose

	
	'use strict'
	
	let koa = require('koa');
	
	let compose = require('koa-compose');
	
	let app = koa();
	
	function* responseTime(next) {
		let start, end, ms;
		start = new Date();
		yield next;
		end = new Date();
		ms = end - start;
		this.set('X-response-Time', ms + 'ms');
	}
	
	function* logger(next) {
		let start, end, ms;
		start = new Date();
		yield next;
		end = new Date();
		ms = end - start; 
		console.log(`${this.method} ${this.url} - ${ms}ms`);
	}
	
	function* respond(next) {
		yield next;
		if (this.url !== '/') {
			return;
		}
	
		this.body = 'Hello, DR!';
	}
	
	// app.use(responseTime);
	// app.use(logger);
	// app.use(respond);
	
	app.use(compose([
		responseTime,
		logger,
		respond
		]));
	
	
	
	app.listen(5000);
	
### koa-logger
>  koa-logger中间件的使用 
	
	'use strict'
	
	let koa = require('koa');
	
	let logger = require('koa-logger');
	
	let app = koa();
	
	app.use(logger());
	
	app.use(function* (next) {
		yield next;
		if (this.path === '/') {
			this.body = 'Home Page';
		} else if (this.path === '/about') {
			this.body = 'About Page';
		} else {
			this.body = 'Page Not Found';
		}
	})
	
	
	app.listen(5000);
	
### conditional-middleware
> 条件过滤的中间件

	var logger = require('koa-logger');
	var koa = require('koa');
	var app = koa();
	
	
	// passing any middleware to this middleware
	// will make it conditional, and will not be used
	// when an asset is requested, illustrating how
	// middleware may "wrap" other middleware.
	
	function ignoreAssets(mw) {
	  return function *(next){
	    if (/(\.js|\.css|\.ico)$/.test(this.path)) {
	      yield next;
	    } else {
	      // must .call() to explicitly set the receiver
	      // so that "this" remains the koa Context
	      yield mw.call(this, next);
	    }
	  }
	}
	
	// TRY:
	// $ curl http://localhost:3000/
	// $ curl http://localhost:3000/style.css
	// $ curl http://localhost:3000/some.html
	
	app.use(ignoreAssets(logger()));
	
	app.use(function *(){
	  this.body = 'Hello World';
	});
	
	app.listen(3000);
	
### cookies
> 设置cookies
	
	'use strict'
	
	let koa = require('koa');
	
	
	let app = koa();
	
	app.use(function* (next) {
		yield next;
	
		let n = ~~this.cookies.get('view') + 1;
		this.cookies.set('view', n);
		this.body = n + 'views';
	})
	
	app.listen(5000);
	
	
### error
> 错误处理机制，冒泡机制



	'use strict'
	
	let koa = require('koa');
	
	
	let app = koa();
	
	app.use(function* (next) {
		try {
			yield next;
		} catch(err) {
			this.status = err.status || 500;
			this.type = 'html';
			this.body = '<p>Something <em>exploded</em>, please contact Maru.</p>';
			this.app.emit('error', err, this);
		}
	});
	
	app.use(function* (next) {
		yield next;
		throw new Error('boom boom');
	});
	
	
	app.on('error', (err) => {
		if (process.env.NODE_ENV !== 'test') {
		    console.log('sent error %s to the cloud', err.message);
	    	console.log(err);
		}
	});
	
	app.listen(5000);