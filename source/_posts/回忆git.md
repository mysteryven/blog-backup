---
title: git的一些很有用的命令
date: 2018-12-11 20:53:19
tags: git
---

git rest --hard 是清除工作区和暂存区里面的代码，也就是清除当前未 add，和已经 add 但是没有 commit 的代码
git mv readme readme.md git 重命名的简便方式
git log -n4 --oneline 最近的 4 次
git log --master --graph 图例化
git help --web log 
git config --local user.name 'wenzhe'
gitk -all 图形界面
git checkout -b newBranch 创建新分支并切换到
git diff 比较两个commit 版本
git diff HEAD HEAD^
git branch -d branch 删除分支，如果没有合并 git 会提示，此时再 -D 删除最保险
git commit --amend
git rebase -i 父亲的commitid，来修改一个commit 或者多个
上面那个命令修改多个的时候可能不能直接行，那就 git rebase --continue
git diff --cached 暂存区和 head 指向的 commit 之间的差别
git diff 工作区和暂存区的差别，后面可以加文件名详细的比较文件

git reset HEAD 暂存区的都不要了，还原回工作区
变化工作区用 checkout 变暂存区用reset
git checkout -- index.html 把工作区的文件改为和暂存区一样的

