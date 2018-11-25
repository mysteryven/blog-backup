# 理解Git

> 2018.8.24 晴

在公司用到的VSC是SVN,并且用到的也只是简单的几个命令，昨天我学习了一下Github的一些操作，  觉得很有必要学习一个git了，这对我理解Github的用法也很有帮助，也对我以后有好处。于是我今天从Coursera上注册了一个课程，准备跟随他学习一下Git，笔记将记录在这里.

## 宏观的理解Git

- continuous improvement by commits
- simultaneous(同时) stability and development by branches
- improved quality by pull requests
- git都是以git开头，然后后面接空格
- ![屏幕快照 2018-08-24 上午9.58.01.png](https://i.loli.net/2018/08/24/5b7f664156b51.png)

## 一些不知道但是有用的命令

- git --version 查看版本
- git help init 查看所有的帮助
- git config --global user.name
- git log --oneline -number 输出log只一行 number为指定数量

## 概念

- working tree包含了项目的一次commit的文件、目录
- staging area 通过add添加到里面
- local resposition包含了本地的多次commit
- staging area local在.git这个文件夹里
- remote repository在远程
- git status是查看的work tree 和staging area之间状态
- git add add untracked and modify to staging area
- git commit create snapshot of current project
- git clone 得到local repository，可以指定名字在第二个参数
- git remove -v
- git push [-u] [rep] [branch]
- git push -u origin master 如果当前分支与多个主机存在追踪关系，则可以使用 -u 参数指定一个默认主机，这样后面就可以不加任何参数使用git push

## git 的 DAG 模型

- commit object - a small text file
- Annotaed tag - 特定 commit 的索引
- `git log --oneline --graph` 很好用
- Git IDs 是一个 40 位的 16 进制数，也是 git Object 的名字，Git IDs 通常是四个字母的缩写或者更多的缩写
- git show to show all ids
- git hash-object get file's hash id 
- acyclic means no cycles


## 
