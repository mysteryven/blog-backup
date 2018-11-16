---
title: css花园之堆叠上下文
date: 2018-11-12 22:43:04
tags: css
---

## 堆叠顺序

border 比 background 更靠近用户。

结合 「text-indent」 得知文字 (内联元素) 比 border 更靠近用户。

在 content 区域，内联元素比块级元素的背景高，但是如果在块级元素里面加文字，那就要按照一般的规则，肯定是孩子的内联比父亲的内联高（不加其他因素）。

浮动元素在块级元素和内联元素之间。

relative 在上面（background，border，content）的那些上面。

只有被定位的才能使 z-index 生效，z-index 对浮动也不生效，生效了之后只按照 z-index 来定位 （不考虑堆叠上下文）。

正的 z-index 比 所有的都高，而负的 z-index 比 background 还低，也就是最低。


## 堆叠上下文

在同一个堆叠上下文中比较，尽管不在同一级，但是 z-index 仍然起作用。

[在线预览](https://jsbin.com/facowipore/1/edit?html,css,output)

```html
<div class="a">
  <div class="b"></div>
</div>
<div class="c"></div>
```

```css
.a {
  width: 100px;
  height: 100px;
  border: 10px solid red;
  background-color: background;
}
.b {
  width: 50px;
  height: 50px;
  background-color: green;
  position: absolute;
  top: -20px;
  z-index: 11;
}
.c  {
  width: 50px;
  height: 50px;
  background-color: black;
  position: relative;
  z-index: 10;
  top: -120px;
}
```

z-index 不为 auto 的绝对或相对定位就会造成堆叠上下文, html 本身就是最大的堆叠上下文。

出现了堆叠上下文，那内部的元素和外部的元素比较都是建立在此层和外面的元素比较，出现了堆叠上下文，就类似于公司新增了一个部门。

部门内一个人的职位和部门外一个人的职位是无法直接比较的。只能借助两个部门的高低来比较，这个部门高，那此部门的所有人都高，这个部门低，那所有人都低。

有了堆叠上下文之后 负的 z-index 是不会低于堆叠上下文的 border，background 的，可以借助下面这句话理解，background 是当前堆叠上下文的下边界，如果产生了堆叠上下文，内部的元素无论如何也脱离不出去。



以代码的形式总结一下的话，如下:

[在线预览](https://jsbin.com/latanojago/edit?html,css,output)

```html
<div class="a">
  <div class="b"></div>
</div>
```

```css
.a {
  width: 100px;
  height: 100px;
  border: 10px solid red;
  position: relative;
  z-index: 0;
  background-color: background;
}
.b {
  width: 50px;
  height: 50px;
  background-color: green;
  position: relative;
  top: -20px;
  z-index: -999;
}
```

(完)
