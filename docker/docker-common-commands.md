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
$ sudo docker inspect <IMAGE_ID>
```

获取镜像的 Architecture 信息
```
$ sudo docker inspect -f {{".Architecture"}} <IMAGE_ID>
```

搜索带 mysql 关键字的镜像
```
$ sudo docker search mysql
```
