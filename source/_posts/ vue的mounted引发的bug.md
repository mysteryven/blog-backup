---
title: 轮播组件和vue结合的一次bug
date: 2018-12-06 19:55:09
tags: vue
---

这几天我在做vue项目的时候遇到了一个坑，导致我上个周六就没好好做项目，一直到今天才得以解决。

是这样的，我在渲染轮播图的时候，一直出现加载到了数据但是无法滑动的情况，当我换成静态的数据就有办法滑动了，这让我很费解。后来我询问了一个朋友，他帮我解决了，原因如下：

我在还没获取完数据就把轮播初始化了。

额，对就是这么简单，我把轮播放到 mounted 里面了，尽管我是在 created 的生命周期里请求的数据，但是当所有的dom节点都加载完成了，数据还没请求完毕，而这时候轮播已经初始化了。知道这个原因之后，我把初始化轮播的操作放到请求完数据的 nexttick ，然后就成功了！

我去，这是我学习 vue 第一个大坑啊！解决完真开心。

以前都没用过 nexttick ，这次也算是用的恰到好处。

以上
（完）


