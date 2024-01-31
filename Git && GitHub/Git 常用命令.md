# Git 常用命令

## 获取 Git 仓库

- `git clone`：从远程仓库克隆到本地
- `git init`：初始化本地仓库

## 分支

### 创建新分支

`git branch <branch-name>`

### 推送分支到远程仓库

`git push -u <remote> <branch-name>`

### 查看分支

`git branch`

### 删除分支

`git branch -d <branch-name>`

### 创建并切换到新分支

`git checkout -b <branch-name>`

## 仓库状态

`git status`







**git pull** 命令用于从远程仓库获取更新。此命令是 **git fetch** 和 **git merge** 的组合。这意味着，当我们使用 git pull 时，它将从远程仓库（git fetch）获取更新，并立即在本地应用最新更改（git merge）。

