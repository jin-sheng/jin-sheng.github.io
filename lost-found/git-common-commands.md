# Git 常用命令

克隆 git 源代码仓库
```shell
$ git clone https://github.com/git/git.git
```

基于 master 分支创建并切换到新的分支 master_hotfix
```shell
$ git checkout master
$ git checkout -b master_hotfix
```

本地的 master 分支推送到 origin 主机，同时指定 origin 为默认主机（后面就可以不加任何参数使用 git push 了）
```shell
$ git push -u origin master
```

更新本地仓库中的所有远程分支，删除所有远程上不存在的分支
```shell
$ git fetch -p
```

拉取 origin/master 远程分支的最新信息并合并到本地 master 分支
```shell
$ git checkout master
$ git pull
# 等价于
$ git fetch
$ git checkout master
$ git merge origin/master
```

改写 master 分支的本地历史，将 HEAD 指向 becd81c9 这次提交
```shell
$ git checkout master
$ git reset --hard becd81c9
```

改写 master 分支的远程历史，撤销 becd81c9 这次提交
```shell
$ git checkout master
$ git revert becd81c9
$ git push
```

将分支 master_hotfix becd81c9 这次提交复制到 master 分支
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

显示历史记录时，每个提交的信息只显示一行（默认 medium）
```shell
$ git config format.pretty oneline
$ git log
```

# 参考
[git 简明指南](https://www.runoob.com/manual/git-guide/)<br>
[PRETTY FORMATS](https://git-scm.com/docs/pretty-formats/2.11.4)<br>
[Learn Git Branching](https://learngitbranching.js.org/)
