---
title: 使用vue-cli来构建单页面应用或多页面应用.md date: 2018-11-14 21:36:17
tags: vue 
---

# 单页面应用配置

## 安装 vue-cli

```shell
yarn global add @vue/cli

yarn global add @vue/cli-service-global
```

## 初始化项目

`vue create hello-world`

## 运行项目

```
yarn serve
yarn build
```

## 配置

如果我如下配置，当我运行 `yarn build` ，我将在项目的根目录下得到一个 dist1 文件夹，并且，我能在此目录下打开 test.html 而不会发现找不到 css、js 链接的情况。

原因在于我使用了 ./ 的 baseUrl。当然，我也可以使用 /dist1/。

```js
# vue.config.js
module.exports = {
  baseUrl: './',
  outputDir: 'dist1',
  indexPath: 'test.html'
}
```

# 多页面应用配置

接着上面单页面的配置，我们来进行多页面应用的配置。

在 vue-cli 2 的时候，配置好像还蛮麻烦的，只是我没有配置过。我在配置 vue-cli 3 的时候感觉很简单，我们几乎不需要什么操作，基本目录结构和配置文件如下所示：

```
hello-vue
  src
    assets
    components
    footer
      footer.html
      footer.js
    index
      index.html
      index.js
  ...
  dist
```

```js
# vue.config.js

const baseUrl = '/dist/'
module.exports = {
  baseUrl: baseUrl,
  runtimeCompiler: true,
  pages: {
    index: {
    entry: 'src/index/index.js',
    template: 'src/index/index.html',
    filename: 'index.html',
    title: 'Index page',
    },
    footer: {
      entry: 'src/footer/footer.js',
      template: 'src/footer.html',
      filename: 'footer.html',
      title: 'footer page',
    }
  },
  devServer: {
    historyApiFallback: {
      proxy: 'http://localhost:8080/dist'
    }
  }
}
```

需要注意的一点就是「devServe」。

我的 baseUrl 是 dist 目录，并且 *.html 也是 dist 的直接子目录， 所以可以直接这样写。这样写了之后我就能在这些页面之间跳转了。

在网上，我还看到了另外一个人的 devServer 的做法，原理是一样的，都是因为如果不设置 devServer 的话，浏览器就没有返回的东西。

```
devServer: {
  historyApiFallback: {
  rewrites: [
  { from: /\/index/, to: '/index.html' },
  { from: /\/footer/, to: '/footer.html' }
  ]
  }
}
```

## alias 

```
 configureWebpack: {
    resolve: {
      alias: {
        'assets': '@/assets',
        'components': '@/components',
        'css': '@/modules/css',
      }
    }
  },
```

写到这里，关于 vue-cli 的使用已经基本介绍完毕了，后续可能会补充一些小的细节吧！

（完）

