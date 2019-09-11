---
layout: post
title: "ubuntu git安装"
date: 2019-07-20
tags: 工具  
---
# ubuntu git安装

## 安装：

```
1. 首先尝试输入git，看看系有没有安装git
2. 安装git：sudo apt-get install git
```



## 创建版本库：

```
选择一个地方创建一个空目录：
$ mkdir mygit
$ cd mygit
$ pwd
/home/xiao/home/mygit

把这个目录变成git管理的仓库
$ git init
已初始化空的 Git 仓库于 /home/xiao/home/mygit/.git/
```



## 添加文件到版本库：

```
mygit目录下编写一个readme.txt文件，
把文件添加到仓库：$ git add readme.txt
把文件提交到仓库：$ git commit -m "this's a new file" (-m后面输入的是本次提交的说明)
查看结果: $ git status
查看具体修改的内容：$ git diff
重新提交：add -> commit -m -> status检查
```



## 版本回退：

```
历史纪录：$ git log
历史纪录(精简版)：$ git log --pretty=oneline
回到过去：$ git reset --hard HEAD^
查看文件： $ cat readme.txt

历史命令，以查看版本号： $ git reflog
重返未来：$ git reset --hard (版本号)
注：HEAD指向的版本就是当前版本
```



## 撤销修改：

```
没有添加到暂存区时：$ git checkout -- readme.txt
没有提交时：$ git reset HEAD readme.txt   ->    重复第一步
提交后没有推送到远程：版本回退
```



## 删除文件：

```
删除版本库文件：$ git rm person.txt  ->  git commit -m ""
还原删除的文件(前提是版本库有)：$ git checkout -- person.txt
```



## 远程仓库：

```
1. 创建SSH密钥：ssh-keygen -t rsa -C "13546680704@163.com"
    检查：在用户主目录里找到.ssh目录，看看这个目录下有没有id_rsa和id_rsa.pub这两个文件
2. 登陆GitHub，“SSH and GPG Keys”页面：
点“New SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容
3. 关联远程库：(远程库的默认名字就是origin)
	$ git remote add origin https://github.com/zcxiao74/xiao.git
4. 把本地仓库的内容推送到GitHub仓库:
	(第一次推送): $ git push -u origin master
	(之后): git push origin master
```



## 从远程库克隆

```
首先，登陆GitHub，创建一个新的仓库，名字叫work
克隆一个本地库 ：$ git clone git@github.com:zcxiao74/work.git
```



## 创建与合并分支

```
创建+切换dev分支：$ git checkout -b dev
创建分支：$ git branch dev
切换分支：$ git checkout dev
查看当前分支：$ git branch
dev分支的工作成果合并到master分支上：$ git merge dev
删除dev分支：$ git branch -d dev
查看当前分支：$ git branch
```



## 解决冲突

```
准备新的dev分支: $ git checkout -b dev
修改readme.txt后提交： git add  ->  git commit
切换到master分支：$ git checkout master
修改readme.txt后提交： git add  ->  git commit
合并：$ git merge dev (此时合并冲突)
cat readme.txt 参看并修改冲突
查看分支合并情况：$ git log --graph --pretty=oneline --abbrev-commit
查看分支图：$ git log --graph
删除dev分支：$ git branch -d dev
```



## 分支管理策略

```
		如果要强制禁用 Fast forward 模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
		
创建并切换dev分支: $ git checkout -b dev
修改提交新的commit:  git add  ->  git commit
切换master: $ git checkout master
合并dev分支(禁用Fast forward)：$ git merge --no-ff -m "merge with no-ff" dev
查看历史分支：$ git log

		合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
```



## Bug分支

```
储藏当前工作：$ git stash
被储藏的仓库：$ git stash list
恢复：$ git stash apply
删除：$ git stash drop
恢复并删除：$ git stash pop
```



## Feature分支

```
开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
```



## 多人协作

```
查看远程库： $ git remote
查看远程库： $ git remote -v
推送分支：$ git push origin master
多人冲突后，远程抓取分支：$ git pull

如果 git pull 也失败了，原因是没有指定本地 dev 分支与远程 origin/dev 分支的链接，根据提示，设置 dev 和 origin/dev 的链接：

关联远程分支：$  git branch --set-upstream-to=origin/dev dev
本地创建 与远程对应的分支：$ git checkout -b dev origin/dev
远程抓取分支：$ git pull
git pull成功，但是合并有冲突，需要手动解决，
再合并：$ git commit -m "fix env conflict"



多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。
```



## Rebase

```
把本地未push的分叉提交历史整理成直线：$ git rebase

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
```



## 标签管理

```
切换分支：
​		$ git branch
​		$ git checkout master

创建标签：$ git tag v1.0
精准打标签：$ git tag v0.9 (版本号commit id)
历史commit id : $ git log --pretty=oneline --abbrev-commit
创建带说明的标签：$ git tag -a (tag) -m "" (commit id)

查看所有标签：$ git tag
查看标签信息：$ git show v0.9
```

```
删除标签：$ git tag -d (tag)
推送标签到远程： $ git push origin (tag)
推送全部标签到远程： $ git push origin --tags
删除远程标签：
​		先从本地删除：$ git tag -d (tag)
​		再从远程删除：$ git push origin :refs/tags/(tag)
```

