# Git指南

将常用的命令进行总结

## git 基础配置

- `mkdir 文件夹名` 创建文件架
- `touch <flie>` - 创建文件
- `ls` 查看当前文件夹下的文件列表
- `code <flie>` 在编辑器中打开文件, *此处需要配置编辑器为vscode*
- `ctrl + L` 清屏
- `git config --global user.name "You Name"` 设置全局用户名
- `git config --global user.email johndoe@example.com` 设置全局邮箱
- `git config --global -e` - 查看git全局配置文件
- `git config --global core.editor "code -w"` - 配置git默认的编辑器，vscode
- `git config --global alias.a add` - 配置全局命令别名，简化操作如：*a = add*

#### 使用系统别名配置git全局指令
打开用户下的.bash_profile文件，加入以下指令

``` c++
alias gs='git status'
只要在命令行使用 gs 即可查看状态
```

---

## 获取Git仓库的两种方式

1. 在本地创建仓库,`git init`
2. 获取远程仓库, `git clone <url>` url为*远程仓库地址*[^1]

#### 配置密钥

1. 生成密钥`ssh-keygen`,生成的密钥保存在user下的.ssh文件夹,将**公钥**复制
2. 在github的Settings中选择SSH and GPG keys,添加密钥

现在可以进行克隆，推送，拉取等操作
[^1]: 一般使用github，在code里面选择ssh地址

---


## 更新仓库

- `git status` 检查文件状态
- `git add .` 将文件放入暂存区
- `git commit -m "提交信息"` 提交到本地库
- `git commit -am "提交信息"` 将已追踪的文件提交到本地库，*跳过add*

#### 忽略文件.gitignore

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件的模式。要养成一开始就为你的新仓库设置好 .gitignore 文件的习惯，以免将来误提交这类无用的文件。**正则表达式**

#### 移除文件

- `git rm <file>` 移除文件，会删除本地目录的文件
- `git rm --cached <file>` - 仅删除本地库文件，**保留**本地文件
- `git mv <file> <new file>` 重命名

#### 查看提交历史

- `git log` 查看日志
- `git log -p -2` 查看日志,显示每次提交所引入的差异,限制为两条

---
  
## Git撤销操作

- `git commit --amend` 重新提交
  > 如果暂存区没有文件，只是修改了提交信息
  > 如果暂存区有文件，会一起提交，上一次的提交会被这次的替换掉
- `git reset HEAD <file>` 将修改的文件从暂存区撤回，修改的文件内容**不变**
- `git restore --staged <file>` 撤销当前操作将文件恢复到工作区，修改的文件内容**不变**
- `git checkout -- <file>` - 将文件回复到最近一次的commit，文件内容**恢复**到修改前

---

## 远程仓库操作

- `git remote -v` 查看已配置的远程仓库
- `git remote add <shortname> <url>` 添加远程仓库
- `git remote rename oldName newName` 修改远程仓库别名
- `git fetch <remote>` 拉取数据，但不会合并到当前分支
- `git pull <remote>` 拉取数据，**自动合并**到当前分支
- `git push <remote> <branch>` 推送到远程仓库
- `git remote show <remote>` 查看远程仓库信息

---

## 打标签

标签只适合用于功能开发完成的项目，不可以随意打标签。

- `git tag -l` 查看已有的标签列表
- `git tag -l "筛选标签"` 使用正则来筛选，eg: "v1.8.5*"
- `git tag -a v1.0 -m "my version 1.0"` 创建附注标签
- `git tag v1.2` 创建轻量标签
- `git show <tag>` 标签信息和与之对应的提交信息，*轻量标签*只能看见提交信息
- `git tag -d <tagname>`删除标签

## 分支

- `git branch` - 查看所以分支
- `git branch <branch>` - 创建分支
- `git checkout <branch>` - 切换分支
- `git checkout -b <branch>` - 创建一个新分支，并切换到此分支
- `git merge <branch>` - 在现在的分支上**合并**其他分支
- `git branch -d <branch>` - **删除**分支
- `git branch --no-merged` 查看未合并的分支
- `git rebase <branch>` 移动子分支到最新的主分支，解决bug，分支合并更简单 
