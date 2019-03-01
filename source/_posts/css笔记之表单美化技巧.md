---
title: 表单美化小技巧
date: 2018-12-02 08:50:43
tags: css
---

## 去掉本身的 outline

```
input[type=text]:focus {
  outline: none;
  border-color: blue;
}
```

不要定 input 的宽高，用 padding 的形式做出来
可以通过调节 font-size 来调节光标的大小
高度和行高一样就是居中的
input 会有自动补全功能, autocomplete="off" 可以关掉他

上传文件后立马上传，要监听 input 的 onchange
```js
// search jquery get formData
let formData = new FormData()
formData.append('file', input.files[0])

ajax.....
```

button 会自动上下居中，如果不是的话且文字只有一行可以用 line-height == height 来使它居中
做动画用 visibility 属性`


