# git 同步规则

目前本地仓库连接了两个远程，一个是原作者的git 一个命名为author 一个是命名为origin，aithor是原作者的git仓库，origin是我（baixian）的仓库
可以通过
git remote -v

来查看

由于原作者仍然在同步进行开发，所以拉取流程是这样的

首先本地切换到main分支，该分支用于保存拉取的源码，不要在这个分支上做改动；然后从author远程仓库的main拉代码下来

本地分支切换到主分支
git checkout main

查看远端仓库的分支情况
git branch -a

从远端main拉
git pull author main

本地切换到dev分支
git checkout dev

将main分支合并到dev分支上来
git merge main



