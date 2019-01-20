---
title: 小程序canvas的两个坑
date: 2019-01-11 21:02:12
tags: 小程序
---

1. 显示网络中的图片

```js
getImg(id).then(res => {
    let imgPath = res.xxx // 你的图片路径

    wx.getImageInfo({
          src: imgPath,
            success: (res) => {
              const content = wx.createCanvasContext('myCanvas')
              content.drawImage(imgPath, 0, 0, 150, 100)
              content.draw()
          }
     })
})
```

getImg 是代表异步获取图片链接的代码，小程序比较蛋疼的就是无法把网络地址的图片直接展示在画布上，所以需要我们先获取到图片，再用小程序的方法获取图片的临时链接，最后把临时链接画到画布上。

2. 使用 rpx

```js
wx.getSystemInfo({
  success: (res) => {
    this.setData({
        rpx: res.windowWidth / 375
    })
  }
})
```

小程序的画布是不支持 rpx 的，这一点也很烦，所以需要我们手动写好 rpx 的函数，然后在需要使用单位的地方使用 rpx 得到返回值来使用。


