> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
>
> Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows.
> -- https://git-scm.com/

Git 是一种 VCS (version control system)，用于更好的控制项目的版本分发，处理多人合作项目时容易遇到的问题。一定程度上，现在除了一些大厂因为他们自己的需求不完全使用 Git 之外，都在用 Git 做 VCS。

Git 版本控制的过程可以理解成虚拟机快照，每个 commit 就是一个快照，Git 就是用来帮助开发者管理快照的软件。

常见的 Git 的操作:

```bash
$ git config --global user.name "yourname"
$ git config --global user.email test@mail.com
# 初始化本地git仓库
$ git init
# 提交到暂存区
$ git add
# 提交暂存区至本地仓库
$ git commit
$ git commit -m [message] # 添加备注信息
$ git commit -a # 不用add了
$ git commit --amend # 修复最后一次本地提交，可以避免漏掉少数文件、备注错填等问题，注意不要对已经push的commit使用amend
# 删除文件
$ git rm
# 比较暂存区和本地仓库
$ git diff
# 查看日志
$ git log
# 查看git状态
$ git status
# 管理远程仓库
$ git remote
$ git remote add origin [url] # 配置远程仓库链接
$ git remote set-url origin [url] # 修改远程仓库源
$ git remote rename origin [new-name] # 重命名远程仓库名称
# 拷贝远程仓库
$ git clone
# 从远程获取代码库
$ git fetch
# 拉取远程仓库并合并
$ git pull
# 推送本地仓库并合并
$ git push
# 创建分支
$ git branch # 列出本地分支
$ git branch [branchname]
$ git branch -d [branchname]
# 切换分支
$ git checkout [branchname]
$ git checkout -b [branchname] # 创建并切换到新分支
# 合并分支
$ git merge [branchname] # 将任意分支合并进当前分支
# 若出现冲突，则需手动处理，解决后使用git add告诉Git冲突解决
```

上面这些命令整理摘自 [Git常用命令整理](https://blog.tsio.top/archives/1721013781479)