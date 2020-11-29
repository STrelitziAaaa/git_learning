# git_learning
你应该知道的:
- 默认主分支: main(以前叫master,避免种族歧视改成main)
- 默认远程主机名: origin
- 
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
  - 将当前路径的所有文件加入stage
## git commit
将暂存区提交到仓库,自此一个本地仓库被更新了!
- git commit -m "update readme"
  - 提交此次修改,-m代表message
- git commit --amend
  - 将此次提交覆盖最近的一次提交,常用于修改最近提交的message,事实上,两次提交之间完全可以add新文件
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
f

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

## git pull

## git restore

## git status

## 撤销文件修改
- git checkout .
  - 将当前分支的所有文件还原到stage中文件的状态,如果stage为空,就是最近一次commit的状态; 相当于从index中恢复文件,加入stage就是添加索引
- git checkout [file]
## 移出stage
- git reset 
  - 即 git reset --mixed head~1 (head~1也可以写成head)
  - 将所有add文件移出stage,但不会撤销文件的修改
- git reset head [file]
  - 本质都是--mixed的作用,不撤销对文件的修改,只unstage
  - 将[file]文件移出stage,但不会撤销文件的修改
## 撤销commit/stage
- git reset commitId (默认是--mixed)(可以是commitId,也可以是head~1,代表倒退1个commit)
  - 回到commitId那个版本
  - --mixed unstage,但不撤销对文件的修改
  - --soft 什么都不改变
  - --hard 全部撤销(即相当于全部重置到上一次commit)
## 撤销merge
---
# QA
## Diff between add&commit
If committing is akin to "taking a snapshot", staging is about "composing the shot".   
See: [stackoverflow](https://stackoverflow.com/questions/25351450/what-does-adding-to-the-index-really-mean-in-git)

## Switch branch
在切换分支之前,需要保证所有当前修改的文件都被commit
  - 必须是commit,add是不行的
  - 否则会报错,除非你要切换的分支和当前分支是指向同一个结点

