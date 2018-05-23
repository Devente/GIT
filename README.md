```
1、pwd    --------> 显示当前目录
2、git init   -------->这个目录变成Git可以管理的仓库
3、git add 文件          ------->实际上就是把文件修改添加到暂存区（stage）
4、git commit -m '注释'  ------->实际上就是把暂存区的所有内容提交到当前分支
5、git status   ---------->查看状态
6、git diff  ------------->查看修改内容
git diff HEAD -- 文件名  ----------->查看工作区和版本库里面最新版本的区别
7、git log   ------------>历史记录，查看提交历史，以便确定要回退到哪个版本
git log --pretty=oneline   -------->最近一次提交

8、git reset --hard HEAD^  -------->回退上一次提交
   git reset --hard commit_id  ----->回退到指定的版本
9、git reflog  ---------->操作记录，查看命令历史，以便确定要回到未来的哪个版本
10、git checkout 分支   --------->切换分支
11、git checkout -- 文件名   --------->工作区的修改全部撤销，这里有两种情况
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态(工作区--工作区)
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态(暂缓区--暂缓区)
工作区删除：rm 文件名
暂缓区删除：git rm删掉，并且git commit
git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，
但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

git checkout 文件名   ---->用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。


12、git reset HEAD 文件名   ---------->把暂存区的修改撤销掉（unstage），重新放回工作区(暂缓区--工作区)


git remote add origin git地址   -------->关联一个远程库
git push -u origin master   ----------->推送到远程库
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容
推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，
在以后的推送或者拉取时就可以简化命令git push origin master







```