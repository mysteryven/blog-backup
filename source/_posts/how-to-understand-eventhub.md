---
title: 解释EventHub机制
date: 2018-09-14 21:40:23
tags: js
---

## 前言

在项目中，我们可能会需要两个模块间相互通讯，这时候就需要用到EventHub来处理这个问题.举个例子来说，我们页面的头和内容分别是用两个js文件来写的，这时候如果你想通过点击内容来触发头文件的事件，此时就需要用到eventHub机制。


## 代码实现

```
// eventHub.js
window.eventHub = {
  fnList: [],
  on(name, callback) {
    if (!this.fnList[name]) {
      this.fnList[name] = []
    }
    this.fnList[name].push(callback)
  },
  emit(name, data) {
    this.fnList[name].map((fn)=>{
      fn.call(undefined, data)
    })
  }
}
```

## 举例子来说明

> 我们想实现的功能是这样的: 在点击按钮来让header的数字加1  


```
// index.html
 <header>
    数字:<span id='number'>1</span>
  </header>
  <main>
    <button onclick='mainJs.addOne()'>加1</button>
  </main>  



/* js 部分 */
// 我们就这样来假装两个文件了 
var headerJs = {
  run() {
    window.eventHub.on('addOne', (number)=>{
      document.getElementById('number').innerHTML = number
    })
  }

}
headerJs.run()


var mainJs = {
  num: 1,
  addOne() {
    window.eventHub.emit('addOne', this.num++)
  }
}
```

<img src='https://i.loli.net/2018/08/17/5b7624f902c78.png'>

我疯狂加了15次 结果就如上图所示。

## 在vue中的应用

> vue中直接替我们写好了on和emit函数，使用方法是类似的，同样的我们在例子中来理解这个过程。

首先，我们知道组件内部的input的值单单使用v-model的双向绑定无法直接传到外部，此时我们就需要一些tricks。即用eventhub和监听组件内部的input输入事件来解决，具体如下。

<script async src="//jsfiddle.net/0z8gnpv1/17/embed/"></script>

我试用了一下jsfiddle的分享功能，但是浏览的时候由于网速的关系吧，可能不是很理想，所以再paste源码到这



```
 <div id='app'>
    内部:<editable-span v-on:updata='updataName' v-bind:name='name'></editable-span> 
    <hr>
   外部:{{name}}
  </div>
   <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.js"></script>
```


 
```
Vue.component('editable-span', {
	props: ['name'],
	template: `
  	<input :value="name" @input="updataName">`,
  methods: {
  	updataName(e){
    	this.$emit('updata', e.currentTarget.value)
    }
  }
    
})

new Vue({
	el: '#app',
  data: {
  	name: ''
  },
  methods: {
  	updataName(e) {
    	this.name = e
    }
  }
})
```

效果
<img src='https://i.loli.net/2018/08/17/5b763aef6f9b8.png'>

(完)
