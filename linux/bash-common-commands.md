# Bash 常用命令

查看本机的 Bash 版本
```shell
$ bash --version
```

## 基本语法
在屏幕输出 hello world
```shell
$ echo hello world
```

每行列出一个文件
```shell
$ ls -l
```

只有 cat 命令执行成功，才会继续执行 ls 命令
```shell
$ cat filelist.txt && ls -l filelist.txt
```

只有 mkdir foo 命令执行失败（比如 foo 目录已经存在），才会继续执行 mkdir bar 命令
```shell
$ mkdir foo || mkdir bar
```

查看 echo 命令的所有定义
```shell
$ type -a echo
```

## 模式扩展
匹配单个字符
```shell
$ ls ?.txt
```

匹配两个字符
```shell
$ ls ??.txt
```

匹配三个字符
```shell
$ ls ???.txt
```

# 快捷键
清除屏幕并将当前行移到页面顶部
```
Ctrl + L
```

关闭 Shell 会话
```
Ctrl + D
```

# 参考
[Bash 脚本教程](https://wangdoc.com/bash/index.html)  
