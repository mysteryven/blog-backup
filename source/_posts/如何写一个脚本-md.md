---
title: 如何写一个脚本.md
date: 2018-11-20 22:26:42
tags: 技巧
---

## 什么是脚本

我们在 terminal 运行的 cd，ls，clear 这些都是脚本。

由于进入目录、列表目录、清空控制台这些需求比较常见，所以系统为我们预设了这些脚本。

## 用途

脚本的功能很强大，可以帮我们做一些机械的工作。只是预设的脚本功能比较有限，
但不必失望，我们可以通过自己动手写一些自定义脚本来丰富它，并且，它很简单。

## 示例

我们通过示例来说明如何写一个脚本。

接下来实现的功能是这样的：我想只输入 `new hello` 就能帮我建一个 hello.html，并且每个 html 写入固定的模板。

我把脚本都放到了本地 「~/scripts」 文件夹里面。


1. 新建文件 「new」，同时新建一个 「index.html」，在 「index.html」 里面写入任意内容

2. 打开 「new」，并写入以下内容

```shell
if [ -d $1.html ]; then
    echo 'error: file exists'
    exit
fi
touch $1.html
cp ~/documents/repos/scripts/index.html $1.html
echo 'successfully created'
exit
```

3. 保存退出，并添加权限 `chmod +x new`

4. 在 「~/.bashrc」 文件夹的最后添加这个脚本的路径，比如我的路径是：

     `export PATH="/Users/mac/documents/repos/scripts/:$PATH"`

5. 执行 `source ~/.bashrc`

6. 执行 `new hello`

7. 恭喜你，完成了。

## 总结

实践往往是理解一个事物最快的方式，希望上面的可以帮助到你。

如果你还想了解其他的例子，请点击[click](https://github.com/mysteryven/blog/blob/master/Notes/note-3.md)

