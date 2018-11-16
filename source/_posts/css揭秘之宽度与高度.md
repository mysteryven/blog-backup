---
title: css花园之宽度与高度
date: 2018-11-10 16:37:58
tags: css
---

## 总结

如何在写 css 的时候经常出现 width、height ，那说明你的 css 不过关。

字体的默认行高是有字体设计师写的，所以才会出现不同字体 div 不一样高的情形。

「font-size」 不影响 div 的高度，「line-height」 影响。

1em 等于两个英文字符，一个汉字。

如果一个单词很长，超越了容器的宽度，默认是不会换行的，除非加连字符或者 「word-break」， div 的宽度不是有字体长度决定的，span 的宽度是由字体长度决定的 span（内联元素）的上下 padding margin 都不影响div的高度。

文档流中，内联元素从左到右，超出之后另起一行，块级元素每次都另起一行。

div 的高度是由它内部文档流中元素的总和决定的。

脱离文档流之后，div 的高度将不计入它。

使用上下 padding 相等来使 div 垂直居中

## 汉字对齐

```html 
<span>姓名</span><br>
<span>联系方式</span>
```

```css
span {
  width: 4em;
  text-align:justify;
  display: inline-block;
  border: 1px solid black;
  overflow: hidden;
  height: 24px;
  line-height: 24px;
}
span::after {
  content: '';
  display: inline-block;
  width: 100%;
}
```

## 超出隐藏

搜索关键词 `css multi line text ellipsis`

## 文字垂直居中 

```css
span {
  line-height: 24px;
  padding: 8px 0px;
}
```

## margin 合并

如果父元素没有 border、 padding 来挡住子元素的 margin ，会使父子上下 margin 合并。

##  实现 1:1 的 div

`padding-top: 100%`

(完)
