---
title: generator 模拟 async/await 语法 
date: 2019-11-05 10:07:36
tags: js
---

首先我们有一个 ajax 请求：
```js
function doTask() {
  return new Promise((resolve, reject) => {
    setTimeout(()=> {
      resolve('hello world');
    }, 1000)
  })
}
```

如果用 `async/await` 来写，可以很方便的写成下面这样：
```js
async function init() {
  const res = await doTask();
  console.log(res) // hello world
}
```

我们怎么使用迭代器的语法写出来呢？

接下来我们需要一个 runner 函数来运行它，这是最主要的：

```js
function runner(genFn) {
  const itr = genFn();

  function run(arg) {
    const res = itr.next(arg);

    if (result.done) {
      return result.value
    } else {
      return Promise.resolve.(result.value).then(run);
    }
  }

  return run();
}

function* init() {
  const res = yield doTask();
  console.log(res)
}

runner(init); // hello world
```


我之前一直不理解为什么 `const res = yield doTask()` 为什么能拿到返回值，后来才注意到放到 `itr.next` 的参数。yield 的返回值就是前一步的 next 括号里面的值。

[原文](https://hackernoon.com/async-await-generators-promises-51f1a6ceede2)  