---
title: BFC的作用
date: 2018-12-01 20:51:07
tags: css
---

Block formatting content

如何创建 BFC ?

父元素 float、absolute、inline-block、overflow 不为 visible
diplay: table-cell、flow-root 等
display: flow-root 只有一个触发 BFC 的功能

它可以把内部的元素都包起来，也可以和同级的其他元素划清界限
最好不要用 BFC 来清除浮动，会有副作用

BFC 实在不常用，我只用到过一次，比较实用的一个功能就是可以去掉父子元素的 margin 合并，
但是由于除了 flow-root ，其他属性都有未知的副作用，而flow-root浏览器的支持不太好。所以还是不要用的好，解决 margin 合并的话
可以用 padding、border 来挡住。

总结一下，BFC 完全可以不使用！

(完)






