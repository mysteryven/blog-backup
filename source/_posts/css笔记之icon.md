---
title: css笔记之页面中icon的引入
date: 2018-12-01 16:00:56
tags: css
---

## tips 

图片不要同时写宽和高，只要写了宽这一个属性，他会按照以前图片的比例自适应宽高的。

## ps 导出单一图标

如果设计师给你一张大的 PSD 格式的图片，可以按照以下步骤导出单个图标:
选中图层 -> depulicate layer(选择 new) -> (image-trim)
后续可以在 PS 调整 image 的 size


> 下面讲述页面引入 icon 的几种方法。

## img 

优点是可以自适应宽高比例，写起来也很简单。

## background 

设置 inline-block, width, height 即可

## css sprites 

网上搜索 「css sprites generator」即可，但是我以前都没听过。

## iconfont

它的原理是把字体设计成图标，比如一个字体的编码 &111，它来表示 A，现在字体设计师为了表示一个微信图标，完全可以
在他设计的字体中用 &111 来表示微信图标。
iconfont 默认以 &xe 表示,因为这一段 unicode 编码不表示任何字符。

依据上面的原理，要使用 iconfont 的话，就是先引入 「字体」，然后为引入图标的容器设置 font-family，等等....
具体按照其网站的操作即可，这就是 unicode 方式生成的原理。

也可以再 css 的伪类引入，如果 html 编码 &ex111, 在 css 写 \111，这就是 font-class 生成的原理 
改变大小可以通过调节 font-size。

svg 的方式才是现在的主流, 使用时要点击一下使用帮助，svg 的方式很好，可以使用其描边、填充，使用的时候可以查一下
svg 的用法。

## 纯 css 实现图标

搜索 [css icon](https://cssicon.space/#/)，用 css 实现了很多图标，是 css 快速进步的一个好方法。

## 总结

好了！其实这一篇笔记很简单，甚至没有做笔记的必要，但是还是当做 web 引入 icon 的方式的记录吧。

(完)






