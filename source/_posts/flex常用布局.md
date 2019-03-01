---
title: flex实现几种常用的布局
date: 2018-03-26 16:54:47
tags: css
categories: 编程

---

## 目录
1. 手机布局
2. 九宫格布局 
3. 双飞翼
4. 完美居中


<!--more-->


### 手机布局
<div>
<img src='https://i.loli.net/2018/03/26/5ab8b52083b73.png'
    width="300px" height='500px'
>
</div>

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    ul, li {
  list-style: none;
  margin: 0;
  padding: 0;
}
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}
header {
  height: 100px;
  background: black;
}
footer {
  height: 100px;
}
main {
  flex-grow: 1
}
footer ul {
  display: flex;
  justify-content: space-between;
  height: 100px;
}
li {
   background: #efefef;
   border: 1px solid black;
   width: 25%;
   height: 100%;
}
  </style>
</head>
<body>
  <div class="container">
    <header></header>
    <main></main>
    <footer>
      <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </footer>
  </div>
</body>
</html>

```

### 2. 九宫格布局

<div>
<img src='https://i.loli.net/2018/03/26/5ab8b88b35039.png'
    width="300px" height='500px'
>
</div>

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .parent{
      width: 300px;
      border: 3px solid red;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between
    }
    child {
      width: 90px;
      height: 90px;
      border: 1px solid black;
    }
  </style>
</head>
<body>
  <div class="parent">
    <child></child>
    <child></child>
    <child></child>
    <child></child>
    <child></child>
    <child></child>
    <child></child>
    <child></child>
    <child></child>
  </div>
</body>
</html>
```
### 双飞翼

<div>
<img src='https://i.loli.net/2018/03/26/5ab8d4ce37368.png'
    width="300px" height='500px'
>
</div>

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .parent {
      display: flex;

    }
    .child1 {
      width: 100px;
      height: 100px;
      background: green;
      order: 3;
    }
    .child2 {
      width: 200px;
      height: 100px;
      order: 2;
    }
    .child3 {
      height: 100px;
      width: 100px;
      background: green;
      order: 1;
    }
  </style>
</head>
<body>
  <div class="parent">
    <div class="child1">1</div>
    <div class="child2">2</div>
    <div class="child3">3</div>
  </div>
</body>
</html>
```


### 完美居中

![Screen Shot 2018-03-26 at 7.14.43 PM.png](https://i.loli.net/2018/03/26/5ab8d636c8771.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .parent {
      border: 1px solid red;
      width: 300px;
      height: 400px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
</head>
<body>
  <div class="parent">
    <div class="child">
      I am wenzhe
    </div>
  </div>
</body>
</html>
```
