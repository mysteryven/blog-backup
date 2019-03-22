---
title: 继承的两种写法
date: 2019-03-18 20:39:16
tags: js
---

前几天去面试的时候被问到了这个问题，今天来重新整理一下，并比较一下二者的区别。

如果使用 ES5 ，写起来还挺麻烦的。

```
function Animal(name) {
  this.name = name
}

Animal.prototype.run = function() {
  console.log('Hi, I am ' + this.name)
}

function Dog() {
  Animal.apply(this, arguments)
  this.age = 12
}

var f = function(){}
f.prototype = Animal.prototype
Dog.prototype = new f()

let dog = new Dog('xxx')
dog.run()
```

如果使用 ES6 的 Class 语法，就简单多了。

```
class Animal {
  constructor(name) {
    this.name = name
  }
  run() {
    console.log('Hi, I am ' + this.name) 
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name)
    this.age = 12
  }
}

let dog = new Dog('xxx')
dog.run()
```

上面实现的效果完全相同。   

其实 class 只是一个语法糖而已，它能实现前一种写法一样的功能。可能你会想，既然 class 的写法简单并也没什么不能做的，那我只学 class 就好了，还学原型的写法干什么？其实两种写法都有优劣。首先，只学 class 并不能了解继承的本质，另外，在某些情况下，class 并不简便。

比如，我们想给 Animal 的原型上面添加一个字段而不是方法，用 ES5 我们只需要写 `Animal.prototype.xxx = 'yyy'` 即可，但是在 class 那种写法就要麻烦一点了。

```
get xxx() {
  return 'yyy'
}
```

很多相对立的东西都可以采用「二元论」的策略去认识。大的如同 Vue 和 React，小的如同 JS 继承的两种写法，它可以让我们快速抓住事物的本质并快速的学会。我想很多人都会这么学吧。

（完）