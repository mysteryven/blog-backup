---
title: 手写bind
date: 2019-03-06 09:42:15
tags: js
---

bind 是在 ES5 新加入的语法，具体的语法 MDN 都有。但有一点需要额外注意一下：bind 会返回一个新的函数。也就是说：它会修改 this 的指向，并返回新的函数体。

接下来，我来讲一下手写 bind 的思路。

首先我们要明白 bind 的用途：它是为了改变默认 this 的，如：

```js
var obj = { a: 1 }
function yyy(a) {this.a = a}
var xxx = yyy.bind(obj)
xxx(a) = 3
console.log(obj.a) // 3
```

此时 xxx 的代码实际上是下面这样的

```js
function xxx(newA) {
   obj.a = newA 
}
```
了解了如何使用，我们才能往下写，我们来为函数的原型添加一个 `myBind` 方法

```js
(Function.prototype.myBind = function(otherThis) {
  // 当前的 this 是 yyy，如果 this 的类型不是函数，就返回
  if (typeof this !== 'function') {
    return
  }
  // 获取 yyy 除去第一项后的参数，也就是除去 this 的剩余参数
  var bindArgs = Array.prototype.slice.call(arguments, 1) 
  var bindArgsLength = bindArgs.length  // 这句话很重要，代码后有解释

  var fBind = this // yyy ，也是要绑定到哪里
  var fNP = function(){}  // 中间量，以便生成的 xxx 和原来函数毫无瓜葛
  var fBound = function() {
    bindArgs.length = bindArgsLength // 必须重置 bindArgs 的长度
    bindArgs.push.apply(bindArgs, arguments) // 组合两次的数据

    return fBind.apply(otherThis, bindArgs) // 用 apply 方法为新的返回值绑定用户指定的 this
  }

  if (this.prototype) { // Function.prototype 没有 prototype
    fNP.prototype = this.prototype
  }

  fBound.prototype = new fNP() 
  
  return fBound
})()

```

需要说明一下重置 bindArgs 那一句话：

因为 bindArgs 是和 fBound 同一级别的，当执行 `myBind` 这个函数之后，fBound 和 bindArgs 都只有一份，但是可能多次调用 myBind 返回的函数（这里是 xxx）并传参，如果不重置，我们两次调用 xxx('aaa')，那 bindArgs 的长度就变为 2 了，但我们希望两次调用不能被影响，只能受父亲 yyy 传参的影响。由于每次添加都是 push 到后面，所有每次只要恢复成以前的长度即可。

好了，我们已经大致完成了，但是还要一个缺陷：不支持 new，真正的 bind 方法在使用 new 之后的 this 还是指向 new 新生成的对象。

举例来说，我们希望得到下面的效果：

```js
var obj = { a: 1 }
function yyy(a) {this.a = a}
var xxx = yyy.bind(obj)
var xxxxxx = new xxx('你好')
console.log(obj.a) // 1 
console.log(xxxxxx.a) // 你好
```

而我们现在的代码是如何的呢？ 由于我们没做判断，我们返回的函数实际是：

```js
function xxx(newA) {
   obj.a = newA 
}
```

结果是：xxxxxx.a 未定义，而 obj.a 是你好

如何解决？只需在执行 apply 的时候绑定更换绑定的 this 就好了
解决的关键是 this 到底指向什么，如果使用 new 操作符，那个时候的 this 就是指向新的对象。

```js
(Function.prototype.myBind = function(otherThis) {
  // 当前的 this 是 yyy，如何 this 的类型不是函数，就返回
  if (typeof this !== 'function') {
    return
  }

  var bindArgs = Array.prototype.slice.call(arguments, 1) // 获取 yyy 除去第一项后的参数
  var bindArgsLength = bindArgs.length 

  var fBind = this // yyy ，也是是要绑定到哪里
  var fNP = function(){}  // 中间量，以便生成的 xxx 和原来函数毫无瓜葛

  if (this.prototype) { // Function.prototype 没有 prototype
    fNP.prototype = this.prototype
  } // 放在前面便于理解

  var fBound = function() {
    bindArgs.length = bindArgsLength // 必须重置 bindArgs 的长度
    bindArgs.push.apply(bindArgs, arguments) // 组合两次的数据
      
      // 如果使用 new 操作符，此时 this 指向的是新生成的对象，那么 fNP.prototype.isPrototypeOf(this) === true
      // xxxxxx -> xxx -> FNP
      return fBind.apply( fNP.prototype.isPrototypeOf(this) ? this: otherThis, bindArgs) 
  }

  fBound.prototype = new fNP() 
  
  return fBound
})()
```

写完了，昨天花了一个下午的时间在理解这个问题，我认为理解起来还是有点难度的，希望帮助到你。

（完）



