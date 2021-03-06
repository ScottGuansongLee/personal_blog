---
layout: default
title: Git常用命令2
permalink: /Git常用命令2
excerpt_separator: <!--end-->
---

Git常用命令2-Stashing
=======================
**{{ page.date | date: "%m/%d/%Y" }} Scott**

> 经常有这样的事情发生，当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是[git stash](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning "Stashing and Clean")命令。

- 将当前分支的所有修改存储起来

假设你目前在a分支上开发新功能，开发进行到一半，测试过来找你说有个高优先级的bug需要先修，以往我们先commit我们当前的修改到一个新的分支，然后再checkout一个新分支来修bug，但现在只要输入一下命令，就能直接在该分支上（或切出新分支后）进行开发。

```git
git stash
```

stash将当前所有修改暂存起来，分支暂存区有变干干净净的了。

需要加comment的话

```git
git stash save <comment message>
```

- 查看存储起来的修改

```git
git stash list
```

列出我们所有存在的stash.就像
![loading](/img/WechatIMG70.png "git stash list")

stash@{0}里面的数字类似他们的序号。

- 应用存储

```git
git stash apply stash@{<index>}
```

这样，该条修改便会应用到当前分支上，如果发生冲突，请解决冲突。

git stash apply 之后，我们仍然能够通过```git stash list```的方式查看到该条修改。
如果你不想该条stash还存在，应该使用```git stash pop```的方式。

```git
git stash pop
```

该种方式永远都会将最上面的修改应用到分支上，并且应用之后，该条修改就不存在了。stash pop永远都是取的第一条数据。stash的储存方式有点像栈的模式。

- 清空

```git
git stash clear
```

这样所有的stash都消失了。