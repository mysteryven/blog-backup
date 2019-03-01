---
title: 有点绕的prototype
date: 2018-04-14 21:40:23
tags: js
---

学习JS的原型链有一个公式,记住这个公式,就可以
理清所有的变化了 

> var 对象 = new 函数() 
则 对象的__proto__ === 函数的prototype


关键点还是看`构造这个对象的是什么`


---- 
下面举例:

```
var o = new Object()
a.__proto__ == Object.prototype

var a = new Array(1)
a.__proto__ = Array.prototype

由于Array是一个函数是由Function构造的,所以
Array.__proto__ == Function.prototype

Object 也是一个函数
Object.__proto__ == Function.prototype

Function是一个函数
Function.__proto__ == Function.prototype

Function.prototype 是一个对象,处于顶端了
Function.prototype.__proto__ == Object.prototype

Object.__proto__ === Function.prototype

```
