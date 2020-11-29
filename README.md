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

## git pull

## git restore


## 撤销修改
- git checkout .
  - 将当前分支还原到最近一次commit的状态
---
# QA
## diff between add&commit
> If committing is akin to "taking a snapshot", staging is about "composing the shot". see: [stackoverflow](https://stackoverflow.com/questions/25351450/what-does-adding-to-the-index-really-mean-in-git)

## switch branch
在切换分支之前,需要保证所有当前修改的文件都被commit,否则会报错,除非你要切换的分支和当前分支是指向同一个结点

