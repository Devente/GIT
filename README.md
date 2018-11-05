```
查看远程分支
git branch -a
本地分支
git branch
创建并切换（-b）分支
git checkout -b 分支
把分支推到远程repository
git push origin 分支
删除本地分支
git branch -d 分支
删除远程分支
git push origin :分支
/
git branch -r -d origin/分支



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

13、
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>  ：  -b参数表示创建并切换
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

14、快速合并：看不到分支的commit
我们把dev分支的工作成果合并到master分支上:
git checkout master
git merge dev
git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，
就可以看到，和dev分支的最新提交是完全一样的

普通合并：可以看到分支的commit
git merge --no-ff -m "描述" dev

15、合并冲突
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。

16、修复bug
工作现场：
git status
git stash   ---->把当前工作现场“储藏”起来，等以后恢复现场后继续工作
用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug

git checkout 在哪里修复
git checkout -b issue-101  切换bug分支
git add
git commit -m "fix bug 101"
修复完成后，切换到修复分支，并完成合并，最后删除issue-101分支：
git checkout 在哪里修复
git merge --no-ff -m "merged bug fix 101" issue-101
git branch -d issue-101删除分支
切回现场分支
git checkout dev
工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：
工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
另一种方式是用git stash pop，恢复的同时把stash内容也删了：

再用git stash list查看，就看不到任何stash内容了：
你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：
git stash apply stash@{0}

17、推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。
推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上
git push origin 分支

18多人协作
因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin <branch-name>推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
这就是多人协作的工作模式，一旦熟悉了，就非常简单

18、Tag：注意：标签总是和某个commit挂钩。
命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；用-a指定标签名，-m指定说明文字
命令git tag可以查看所有标签。

命令git push origin <tagname>可以推送一个本地标签；
命令git push origin --tags可以推送全部未推送过的本地标签；
命令git tag -d <tagname>可以删除一个本地标签；
命令git push origin :refs/tags/<tagname>可以删除一个远程标签




```
