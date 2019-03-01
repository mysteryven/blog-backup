---
title: 自己实现jQuery
date: 2018-04-22 10:30:33
tags: jQuery 
---

> 本篇博文来简单的介绍一下jQuery的实现思路

首先我们要明确我们的目的: Dom根本没法用啊, 很多API根本就是摆设,起不到任何作用,
所以于是就想基于Dom写一个好用的库,来提高前端的效率.Jquery就产生了,他依然还是用Dom来操作,
只不过可能我们用jQuery写一句代码,jQuery自己的那个函数要执行十句.总之,jQuery比Dom好用非常多

## 实现过程

##  封装一个函数
以给节点添加class为例
Dom的话
```
var id = document.getElementById('xxx');
id.classList.add('red');
多个的话要一个个的添加
```
发现了不好的地方,我们就要来改进了 
自己实现: 
````
function addClass(node, classes) {
  for (key in classes) {
    let method = classes[key] ? 'add':'remove';
    node.classList[method](key);
  }
}
var xx = document.getElementById('item1');
addClass(xx, {  red: true});
这样我们可以使用addClass,添加多个类,只需给addClass的第二个参数加值就可以了
```

但是上面那样还是不太好 

## 命名空间
我们可能写很多代码,别人怎么知道这是谁写的,怎么才能不和别人的重复
```
var dom = {};
dom.addClass = function (node, classes) {
  for (key in classes) {
    let method = classes[key] ? 'add':'remove';
    node.classList[method](key);
  }
}
```

这样算还可以了,但是我们想更方便,我们为什么还要记录一个命名空间的名字,我们想直接xx.addClass,这样多好

### 能不能把node放到前面
1. 扩展node接口
```
Node.prototype.addClass = function ........
```
这样可以是可以,但是人人都添加的话,那岂不是乱套了?
所以我们总和命名空间和扩展prototype方法的优点和思路,如下:

2. 我们写一个函数 Node2 
```
function Node2(node) {
  return {
    element: node,
    addClass: function (classes) {
        for (key in classes) {
        let method = classes[key] ? 'add' : 'remove';
        node.classList[method](key);
      }
    }
  }
}

// 之后我们可以这样调用了
var xx = document.getElementById('item1');
var node = Node(xx);
node.addClass({red:false})
xx.addClass({red: true})

```

- 给他改一下名字 叫做jQuery就是我们的jQuery啦
```
window.jQuery = Node2
```
- 或者给个简写
```
window.$ = jQuery 
```

### 改进

当然JQuery没有我们上面那个方法那么笨, 他还接受选择器,可以操作多个节点,所以我们要改进一下我们的代码
当然思路还是一样的
我们需要改进什么呢? 
1. 去掉getElementById
2. 操作多个node
3. 添加text函数 获得text命令

```
function jQuery (nodeOrSelector) {
  let nodes = {};
  if (typeof nodeOrSelector === 'string') {
    let temp = document.querySelectorAll(nodeOrSelector);
    for (let i = 0; i < temp.length; i++) {
      nodes[i] = temp[i];
    }
    nodes.length = temp.length;
  } else(nodes instanceof Node) {
    nodes = {0: nodeOrSelector, length: 1};
  }
  
  nodes.addClass = function(classes) {
    for (key in classes) {
      console.log(2)
      let method = classes[key] ? 'add':'remove';
      console.log(nodes.length)
      for (let i = 0; i < nodes.length; i++) {
        console.log(key);
        nodes[i].classList[method](key);
      }
    }
  }
  nodes.text = function(text) {

    if (text === undefined) {
      let content = [];

      for (let i = 0; i < nodes.length; i++) {
        content.push(nodes[i].textContent);
      }
      return content;
    } else {
      for (let i = 0; i < nodes.length; i++) {
        nodes[i].textContent = text;
      }
    }
  }
  return nodes
}

var lis = jQuery('ul>li');
lis.addClass({red:true})

```


### 总结

好了! 经过一步步的改进我们已经很接近jQuery的实现原理了,我们是直接把函数放到JQuery里面
而jQuery是放到prototype里面,我们等以后再更新jQuery!其实到这里就已经很清晰啦,已经明白jQuery实现的原理了!
