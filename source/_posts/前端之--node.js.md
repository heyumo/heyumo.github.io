---
title: 前端之--Node.js
categories:
	一起前端喵喵叫
date: 2020-01-30 16:55:47
notshow: true
---

# 全局对象 global

	__dirname js文件路径  
	__filename 原文件绝对路径

	console.log()
	console.info()

	console.wara()
	console.error()   //日志重定向的时候，默认只会把log和info存储到文件中。 node console.js 1>log.txt 2>&1
	console.time('test')
	for(var i=1;i<100000;i++){}
	console.timeEnd('test') //代码执行时间测试

# process

    process.on()//事件监听
	process.stdout 
	process.stderr
	--用户输入方式：
	process.stdin.setEncoding('utf-8');
	process.stdin.on('readable',function(){
		var data = process.stdin.read();
		console.log(data);
	}) 
	process.cwd();  //执行node命令，当前的路径
	process.stdin.on（'exit' ,function(){
	}）
	process.stdin.on（'SIGINT' ,function(){//改变退出事件
	process.exit();//正常退出
	}）

	process.argv //获取node命令的参数 

# 模块和包	
	require('./xx.js'); 
	require('./xx');//引入某个模块的内容
	模块中的功能：通过赋值exports对象的某个属性提供给调用者
	爆露：module.exports.parse = parse;

	包：文件夹
	package.json: 入口文件。
	通过npm install 来安装包。  通过requrie 来引用。

# 文件操作 -fs -path
	var fs = require('fs');
	fs.readFile('xx.js','UTF-8',function(err,data){
		
	})
	var data = fs.readFileSync('xx.js','utf-8');

	var path= require('path');
	console.log(path.sep)
	console.log(path.extname);//获取文件的后缀
	var http = require('http');
	var server = http.createServer(function(request,response){
	response.end('文字');
	})
	server.listen(8080);
	var url = require('url');
