# GitLearning
你应该知道的:
- 默认主分支: main(以前叫master,避免种族歧视改成main)
- 默认远程主机名: origin
- HEAD指针
  - 你可以认为每一次commit都生成一个node,HEAD指针指向当前分支的最近一次commit对应的node,你也可以直接用当前分支名替代,因为分支名作为指针也总是指向分支的最近一次commit对应的node
- working tree file
  - 工作树文件,即当前在工作区编辑的那些文件
- index/stage
  - 索引区/暂存区,通过git add指令将working tree file加入index/stage,某种意义上,可以认为提交了那个file,因为你可以使用git checkout/restore随时将working tree file 恢复成index中的file了,但这种提交是对其他用户不可见的,真正的对于仓库的提交(对其他用户可见)是git commit
- 文档: https://git-scm.com/docs
# Start a working area
## git init
在本地新建并初始化仓库,生成.git文件
## git clone
- git clone https://github.com/STrelitziAaaa/git_learning.git
将远程仓库clone/copy到本地
# Work on the current change
## git add
将modified/untracked文件加入stage(暂存区)
- git add .
  - 将当前路径的所有文件(包括子文件夹)加入stage
## git commit
将暂存区提交到仓库,自此一个本地仓库被更新了!
- git commit -m "update readme"
  - 提交此次修改,-m代表message
- git commit --amend
  - 将此次提交覆盖最近的一次提交(作为对其的修改),常用于修改最近提交的message,事实上,两次提交之间完全可以add新文件
## git push
将本地仓库与远程仓库同步(推送到远程仓库)
- git push
  - 是git push origin main:main的缩写
- git push origin remote_branch
  - 推送当前分支
- git push origin local_branch:remote_branch
  - 将本地分支推送到远程分支,若远程分支不存在则自动创建
- git push origin :remote_branch_waiting_remove
  - 删除远程分支

## git branch
创建分支
- git branch new_branch
  - 创建新分支
- git branch
  - 显示本repo所有分支,当前分支会带有前导*(比如* main),并高亮
- git branch -a
  - -all 显示所有分支(本地/远程)
- git branch -d local_branch_waiting_remove
  - 删除本地分支
- git push origin -d remote_branch_waiting_remove
  - 删除远程分支(与前面的 : 一样,但显然使用-d,自解释)

## git checkout
切换分支
- git checkout main
- git checkout -b new_branch
  - 创建并切换到new_branch分支, -b:branch

## git merge
合并分支,或者更严格的说,是将其他分支合并进本分支
- git checkout main & git merge dev
  - 切换到main分支,将dev分支合并进main分支
## git rebase
也是合并分支的手段,但是不是直接的merge,而是寻找对方与自己的最近祖先,然后相当于在那个祖先身上先重发对方的commit,再重放自己的commit,这样的commit历史是线性的,而git merge的commit历史是有分支的
- 也许可以认为是线性合并
## git pull
从远程仓库同步本地仓库,先git fetch,再git merge,

## git status
- git status,查看当前的状态
## restore working tree file from index
- git checkout .
  - 将当前分支的所有文件还原到stage中文件的状态,如果stage为空,就是最近一次commit的状态; 相当于从index中恢复文件,加入stage就是添加索引
- git checkout [file]
## unstage
- git reset 
  - 即 git reset . --mixed head~1 (head~1也可以写成head)
  - 将所有add文件移出stage,但不会撤销文件的修改
- git reset head [file]
  - 本质都是--mixed的作用,不撤销对文件的修改,只unstage
  - 将[file]文件移出stage,但不会撤销文件的修改
## git reset的三个参数
- git reset commitId (默认是--mixed)(可以是commitId,也可以是head,代表倒退1个commit)
  - 回到commitId那个版本
  - --mixed unstage,但不撤销对文件的修改(即git restore --staged .)
  - --soft 不改变workingtree和index,只移动head指针到指定commit
  - --hard 全部撤销(即相当于全部重置到上一次commit)(即git restore --staged --worktree .)
## 撤销merge

# EXPERIMENTAL COMMAND
在实验中的命令,行为可能随时改变,不过我认为一般不会有太大的改变了
## git restore
恢复working tree file / index file,用来取代git checkout/reset的部分语义
- git restore .
  - 默认的,从index中恢复当前工作区文件
- git restore --staged(-S) .
  - 取消文件的索引,即撤销git add,不会撤销修改
- git restore --staged(-S) --worktree(-W) .
  - 恢复index文件和working tree文件,即全部回退到上一次commit的状态
  - 相当于git reset --hard
- -S,-W 用来指定恢复的地方,默认恢复working tree from index,如果恢复index,有想恢复working tree,就要两个都显式指定,相当于reset到最近的一次commit
- git restore --sourse(-s) head .
  - 从指定的commit恢复,只更改working tree,即如果你当前index有文件,是仍然存在的
## git switch
切换分支,用于取代git checkout的部分语义
- git switch -c new_branch
  - --create , 即 git checkout -b new_branch 


---
# QA
## Diff between add&commit
If committing is akin to "taking a snapshot", staging is about "composing the shot".   
See: [stackoverflow](https://stackoverflow.com/questions/25351450/what-does-adding-to-the-index-really-mean-in-git)

## Switch branch
在切换分支之前,需要保证所有当前修改的文件都被commit
  - 必须是commit,add是不行的
  - 否则会报错,除非你要切换的分支和当前分支是指向同一个结点,或者使用参数--merge

## 保留空文件夹
.gitignore中如下编写,在a文件夹中加入空的.gitkeep
- 这主要是因为git不会对文件夹track
```
a/*
!a/.gitkeep
```