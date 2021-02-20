# Ubuntu 常用命令

提升用户权限
```bash
$ sudo -i
```

更新软件源和软件列表
```bash
$ sudo apt-get update
```

按照软件源列表中的软件版本进行升级软件安装包版本
```bash
$ sudo apt-get upgrade
```

检查是否有损坏的依赖
```bash
$ sudo apt-get check
```

删除系统中没有使用且无依赖的软件
```bash
$ sudo apt-get autoremove
```

升级系统安装的软件包
```bash
$ sudo apt-get dist-upgrade
```

清理旧版本的软件的缓存
```bash
$ sudo apt-get autoclean
```

清理所有软件的缓存
```bash
$ sudo apt-get clean
```

安装 pip3
```bash
$ sudo apt-get install python3-pip
```

升级 pip3
```bash
$ sudo pip3 install --upgrade pip
```

卸载 pip3
```bash
$ sudo apt-get remove python3-pip
```

使用 apt 安装 git
```bash
$ sudo apt install git
```

# 参考
[Ubuntu系统更新apt安装的软件包](https://blog.csdn.net/qq_36938617/article/details/95234763)  
