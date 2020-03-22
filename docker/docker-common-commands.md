# Docker 常用命令

## 镜像
下载 Ubuntu 14.04 标签的镜像
```
$ sudo docker pull ubuntu: 14.04
```

从 DockerPool 社区的镜像源 dl.dockerpool.com 下载最新的 Ubuntu 镜像
```
$ sudo docker pull dl.dockerpool.com:5000/ubuntu
```

列出本地主机上镜像信息
```
$ sudo docker images
```

获取镜像详细信息
```
$ sudo docker inspect <image_id>
```

获取镜像的 Architecture 信息
```
$ sudo docker inspect -f {{".Architecture"}} <image_id>
```

搜索带 mysql 关键字的镜像
```
$ sudo docker search mysql
```

删除标签为 mysql:latest 的镜像
```
$ sudo docker rmi mysql:latest
```

提交为一个新的镜像
```
$ sudo docker commit -m <message> -a <author> <container_id> <new_name>
```
