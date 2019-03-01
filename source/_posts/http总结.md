---
title: http-summary
date: 2018-03-12 12:18:48
tags: Http
categories: "编程"
---
# 前端需要掌握的Http知识

## 目录
- 请求格式
- 响应格式
- 工具
- 状态码

<!--more-->

## 请求格式
	get / Http1.1
	Host: www.mysterywz.xyz
	User-Agent: 
	accept: */*
	content-type: 

	content

## 响应格式
	HTTP1.1 200 ok
	key-value
	content-type
	content-length
	server

	content

## 查看http请求和响应的工具
1. curl命令  
  curl -s -v -- www.baidu.com
  
2. chrome的network工具条 
  network -- veiw source

## 状态码
1. 2--
	- 200 ok
 	- 201 created
	- 202 accepted
	- 203 服务器是一个转换代理服务器
	- 204 成功处理 但是没返回内容
2. 3--
	- 301 请求的资源被永久移动
	- 302 临时重定向
	- 303对应的请对在另外一个url找到

3. [剩下的](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)








