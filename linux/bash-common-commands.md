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

匹配任意数量的字符
```shell
$ ls *.txt
```

匹配所有 xml 后缀的文件（有几层子目录，就必须写几层星号）
```shell
$ ls *.xml
$ ls */*.xml
$ ls */*/*.xml
```

## 变量
显示所有环境变量
```shell
$ env
```

查看单个环境变量的值
```shell
$ echo $PATH
```

创建变量
```shell
$ custom="hello world"
```

## 算数运算
位运算
```shell
$ echo $((16>>2))
$ echo $((16>>2))
$ echo $((17&3))
$ echo $((17|3))
$ echo $((17^3))
```

逻辑运算
```shell
$ echo $(( (3 > 2) || (4 <= 1) ))
$ echo $((3<1 ? 1 : 0))
```

expr 命令
```shell
$ expr 3 + 2
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

# 其他
查看当前目录下的文件数量（不包含子目录中的文件）
```bash
$ ls -l|grep "^-"| wc -l
```

查看当前目录下的文件数量（包含子目录中的文件）
```bash
$ ls -lR | grep "^-"| wc -l
```

查看服务的 QPS
```bash
$ cat /opt/access.log | grep '服务名称'| awk '{print $2}' | awk -F '.' '{print $1}' | uniq -c
```

显示套接字的内容
```bash
$ netstat -ano
```

## 参考
[Bash 脚本教程](https://wangdoc.com/bash/index.html)  
