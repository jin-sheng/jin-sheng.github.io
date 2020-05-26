# Git 常用命令（Git Bash）

取得项目的 git 仓库
```shell
$ git clone xxx
```

查看仓库状态
```shell
$ git status
```

列出仓库的所有分支，包括远程分支
```shell
$ git branch -a
```

基于 master 分支创建并切换到新的分支 master_hotfix
```shell
$ git checkout master
$ git checkout -b master_hotfix
```

删除本地 master_hotfix 分支
```shell
$ git branch -d master_hotfix
```

删除远程 origin/master_hotfix 分支
```shell
$ git push origin --delete master_hotfix
```

将本地 master_hotfix 分支合并到本地 master 分支
```shell
$ git checkout master
$ git merge master_hotfix
```

把所有文件放入暂存区域
```shell
$ git add .
```

提交，自动暂存已修改和删除的文件，并同时书写 commit message
```shell
$ git commit -am 'hello world'
```

在 master 分支 push 之前修改最后一次提交的 commit message
```shell
$ git checkout master
$ git commit --amend
```

将本地的 master 分支推送到 origin 主机，同时指定 origin 为默认主机（后面就可以不加任何参数使用 git push 了）
```shell
$ git push -u origin master
```

更新本地仓库中的所有远程分支，并删除所有本地存在但远程上不存在的远程分支
```shell
$ git fetch -p
```

拉取 origin/master 远程分支的最新信息并合并到本地 master 分支
```shell
$ git checkout master
$ git pull

# 等价于
$ git checkout master
$ git fetch
$ git merge origin/master
```

改写 master 分支的本地历史，将 HEAD 指向 becd81c9 这次提交
```shell
$ git checkout master
$ git reset --hard becd81c9
```

改写 master 分支的本地历史，将 HEAD 指向 becd81c9 这次提交，同时保留更改的文件
```shell
$ git checkout master
$ git reset --mixed becd81c9
```

改写 master 分支的远程历史，撤销 becd81c9 这次提交
```shell
$ git checkout master
$ git revert becd81c9
$ git push
```

将分支 master_hotfix 的 becd81c9 这次提交复制到 master 分支
```shell
$ git checkout master
$ git cherry-pick becd81c9
```

预览 master 分支与 master_hotfix 分支的差异
```shell
$ git diff master master_hotfix
```

内建的图形化 git
```shell
$ gitk
```

显示历史记录时，每个提交的信息只显示一行
```shell
$ git log --pretty=oneline
```

查看 git 已有的配置信息
```shell
$ git config --list
```

查看 git 作者
```shell
$ git config --global user.name
```

配置 git 作者
```shell
$ git config --global user.name 'xxx'
```

查看 git 邮箱
```shell
$ git config --global user.email
```

配置 git 邮箱
```shell
$ git config --global user.email 'xxx@xxx.xxx'
```

将分支名 master_old 改为 master_new
```shell
$ git branch -m master_old master_new
$ git push origin --delete master_old
$ git push -u origin master_new
```

查看未合并到 master 的分支
```shell
$ git branch --no-merged master
```

查找包含 becd81c9 这次提交的分支列表
```shell
$ git branch --contains becd81c9
```

# 参考
[Git-Book](https://git-scm.com/book/zh/v2)  
[git 简明指南](https://www.runoob.com/manual/git-guide/)  
[Learn Git Branching](https://learngitbranching.js.org/)  
[图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
