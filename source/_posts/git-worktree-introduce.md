---
title: "git worktree 介绍"
date: 2022-04-11 15:54
banner:
tags:
  - git
---

### git worktree 使用场景

如果我们正在feature开发一个新功能，这时候老板说线上有个bug，那么通俗的做法是用git stash保存当前代码，然后从mater拉出一个
hotfix分支，修改提交后再切换到feature分支，用git stash pop恢复之前的代码。

大部分时候可以这么做，但如果遇到大型项目，那么编辑器就会在你切换分支的时候来重新构建索引和设置，将会非常耗时。

还有就是如果我们正在跑测试用例，不想半途而废再重新开始，这时候git stash就不那么灵光了。

git worktree可以在不中断我们任务和当前工程状态情况下帮助我们实现上述场景。

### git worktree操作

`git worktree add -b hotfix ../temp master` 
上述命令就是从当前项目弄出来一个全新的temp目录，并从master分支checkout出一个新的分支hotfix。

后面我们就可以切换到temp目录 `cd ../temp` 用 `git status`查看你会发现这个是干干净净的目录，原来的目录仍然保持当前状态。

在temp文件夹下开发完提交后，就可以切换到我们一开始的目录了。使用`git worktree remove temp`来移除temp副本，至此完成。


### 参考

[https://stackoverflow.com/questions/31935776/what-would-i-use-git-worktree-for/31951225#31951225](https://stackoverflow.com/questions/31935776/what-would-i-use-git-worktree-for/31951225#31951225)

[https://www.gitkraken.com/learn/git/git-worktree](https://www.gitkraken.com/learn/git/git-worktree)

[https://git-scm.com/docs/git-worktree](https://git-scm.com/docs/git-worktree)



