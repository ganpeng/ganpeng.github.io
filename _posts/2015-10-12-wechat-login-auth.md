---
layout: post
title:	基于koa的微信权限认证 
tags: [nodeJS]
---


# 基于koa的微信权限认证

## 1.安装koa和sha1两个npm包
	npm install koa sha1
	
## 2.实现认证的中间件方法
	var checkLoginAuth = function* (next) {
	
		var token, timestamp, signature, nonce, echostr, str, sha1Str;
		token = token;  // 用户在公众号平台配置好的token
		timestamp = this.query.timestamp;  //  微信服务器请求地址中携带的字符串中的timestamp字段
		nonce = this.query.nonce; // 微信服务器请求地址中携带的字符串中的nonce字段
		echostr = this.query.echostr; // 微信服务器请求地址中携带的字符串中的echostr字段, 认证通过后返回给微信服务器
		signature = this.query.signature; // 微信服务器请求地址中携带的字符串中的signature字段, 用来做认证校验
		str = [token, timestamp, nonce].sort().join(''); // 将微信请求中携带的timestamp, nonce 以及公众平台中配置的token，添加到空数组中，然后做字典序排序，最后拼接成字符串
		sha1Str = sha1(str); //  对上一步所得的字符串做sha1加密
		
		if (sha1Str === signature) {   //  将加密后的字符串与signature比较，相等则返回微信服务器echostr，不相等则抛出异常
			this.body = echostr;
		} eles {
			throw new Error('had a problem');
		}
	}
	
	
## 3. 启动服务验证
	var koa = require('koa'),
		sha1 = require('sha1');
		
	var app = koa();
	
	app.use(checkLoginAuth);
	app.listen(5000);
	

	