---
title: css笔记之移动端页面布局
date: 2018-12-01 19:04:15
tags: css
---


## 媒体查询 
语法如下:
```css
@media (min-width: 400px) and (max-width: 800px) {
  body {
    background: red;
  }
}

<link rel="stylesheet" href="./style.css" media="(min-width: 600px) and (max-width: 900px)">
```

有个新闻网站很好的实现了响应式布局: [smashingmagazine](https://www.smashingmagazine.com/articles/)
响应式的本质其实就是做多版，通过媒体查询来选择哪一个

## meta 中 viewport 属性

`html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
`

如果 html 文件里面不加上面那句话，那在手机端的页面宽度就会伪造成 980px，然后根据手机的宽度等比例的把页面宽度缩小。比如 iphone6 的宽度为 375px，那访问同一个页面一个元素的大小变为原来的 375/980。

## 移动端与 pc 的不同

没有 hover
没有 resize 
没有滚动条
有  touch
没有 IE 浏览器！！！

## flex 布局

有一篇非常好的博客 [flex布局](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

##  手机端布局的注意事项

一个小的知识点，给一个没有宽度的块级元素加负 margin，会让他的宽高撑出去。
pc 有滚动条的原因是有宽度，为了避免，要用 width auto
calc属性可以多用一下，比如 `width: (25% -8px)`, 接着设置他们的 margin 为 8，这样不管怎么变，两个元素都是 8px
的间距


(完)









