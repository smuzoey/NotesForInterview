
# Git 简介

&emsp;&emsp;Git是一个分布式版本控制器，是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。
<br>
<br>
<br>

#为什么需要版本控制系统？

&emsp;&emsp;**版本控制**是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。有了版本控制系统，就可以不用担心文件丢失，不小心误修改文件等等“事故”，而且你可以随便回到历史记录的某个时刻。
<br>

&emsp;&emsp;当你用 World 文档写文件时候，保存之后，改着改着想回到最初的版本，往往结果是：回不去！而用 Git 之后，可以将你提交的每个版本都记录下来，你可以退回到提交过的任何一个版本。
<br>

&emsp;&emsp;Git 还可以让多人开发更加方便，比如说我们多人开发时，只能通过互相发送自己的作业而自己进行整合才会得到全部的 work。如果使用 Git ，每个人将自己的完成部分 push 到 Github 远程仓库上，则将会被自动整合。
<br>
<br>
<br>

#Github 与 Git 关系是什么？

Git是版本控制系统，Github是在线的基于Git的代码托管服务。

## Git：
&emsp;&emsp;Git 是一个软件，可在本地建立仓库。例如，你可以在本地写你的 Java 项目的代码，然后用 Git 给它建立一个本地仓库，然后如果在你需要返回之前的版本，就可以使用 Git 的命令，即可返回之前提交的版本。
<br>

## Github：
&emsp;&emsp;Github 是一个专门托管代码并且可以基于 Git 实现版本控制的网站。例如你将你本地仓库上传到 Github 上，你的代码就放到了 Github 网站上，不仅仅是在你的本地上了。所以 Github 还是一个分享代码的地方。
<br>
<br>
<br>

# Git 使用

## Git 操作含义解释

```C
1. git init 
初始化文件，将文件变成可以管理的仓库，在进行此操作后可以看到多了一个 .git 文件，这个文件用来跟踪管理版本库的

2. git add 文件名(包括扩展名)
将文件添加到 Git 仓库中去

git commit -m '提交时的备注'
把文件提交到 Git，-m 后面的内容是对本次提交的说明，方便从历史记录中查看每次提交的原因，然后进行版本回退

git status
查看仓库当前状态

git diff 文件名
查看修改内容
```

## 将本地文件上传到 Github 上
```C
1. 将要上传的文件初始化  git init

2.将文件添加到版本库中(后面有一个点)  git add .

3.将文件提交并提交说明  git commit -m '说明'

4. 关联到远程库   git remote add origin https://github.com/smugit/test.git

5.合并  git pull --rebase origin master
			
6.将本地库内容推到远程  git push -u origin master  会要求输入账户以及密码

7.状态查询  git status
```
<br>
<br>

## Git 回退到之前的版本
```C
查看版本，用于回退使用，最开始前面一长串的就是版本ID
git log --pretty=oneline

恢复到历史版本
git reset --hard 版本id

将修改推到远程服务器
git push -f -u origin master
git pull
```
<br>
<br>

## Git 分支的使用
```C
查看分支 git branch

创建分支 git branch name

切换分支：git checkout name

创建+切换分支：git checkout -b name

合并某分支到当前分支：git merge name

删除分支：git branch -d name

```

<br>
<br>
<br>

# 参考文档
廖雪峰 Git 教程
《Git 团队协作》 中国工信出版集团