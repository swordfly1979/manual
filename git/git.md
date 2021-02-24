# Git常用命令

## 本地操作

git init：初始化本地库
git status：查看工作区、暂存区的状态
git log :查看本地仓库提交记录
git add <file name>：将工作区的文件添加到暂存区(git add . 将所有文件添加到暂存区)
git commit -m "提交日志" ：文件从暂存区提交到本地仓库
git commit --amend 修改最后一次提交的日志说明
git rm --cached <file name>：移除暂存区的文件(文件还未提交到版本库)
git reset HEAD <file name>：移除暂存区的文件（文件已经提交过）
git checkout -- <file name> ：用版本库最后一次提交的文件替换工作区同名文件（文件更改撤消，-- 与文件名有空格）



## 分支操作

git branch 查看分支
git branch <branch name>创建分支
git branch -d <branch name> 删除分支
git checkout <branch name>切换分支
git merge <branch name> 将<branch name>分支合并到当前分支
git branch --merged 查看已经合并到当前分支的所有分支
git branch --no-merged 查看还末合并到当前分支的所有分支



