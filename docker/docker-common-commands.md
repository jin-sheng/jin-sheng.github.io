# Docker 常用命令

## 镜像
下载 Ubuntu 14.04 标签的镜像
```
$ docker pull ubuntu: 14.04
```

从 DockerPool 社区的镜像源 dl.dockerpool.com 下载最新的 Ubuntu 镜像
```
$ docker pull dl.dockerpool.com:5000/ubuntu
```

列出本地主机上镜像信息
```
$ docker images
```

获取镜像详细信息
```
$ docker inspect <image_id>
```

获取镜像的 Architecture 信息
```
$ docker inspect -f {{".Architecture"}} <image_id>
```

搜索带 mysql 关键字的镜像
```
$ docker search mysql
```

删除标签为 mysql:latest 的镜像
```
$ docker rmi mysql:latest
```

提交为一个新的镜像
```
$ docker commit -m <message> -a <author> <container_id> <new_name>
```

导出本地的 ubuntu:14.04 镜像为文件 ubuntu_14.04.tar
```
$ docker save -o ubuntu_14.04.tar ubuntu:14.04
```

从文件 ubuntu_14.04.tar 导入镜像到本地镜像
```
$ docker load < ubuntu_14.04.tar
```

保存为一个新的 sshd:ubuntu 镜像
```
$ docker commit <container_id> sshd:ubuntu
```

使用当前目录中的 Dockerfile 创建自定义镜像
```
$ docker build -t custom:dockerfile .
```

## 容器
新建一个容器
```
$ docker create -it ubuntu:latest
```

启动一个 bash 终端
```
# -t 让 Docker 分配一个伪终端并绑定到容器的标准输入上
# -i 让容器的标准输入保持打开
$ docker run -t -i ubuntu:14.04 /bin/bash
```

终止一个运行中的容器
```
$ docker stop <container_id>
```

启动处于终止状态的容器
```
$ docker start <container_id>
```

重新启动一个容器
```
$ docker restart <container_id>
```

进入一个运行中的容器并启动一个 bash
```
$ docker exec -ti <container_id> /bin/bash
```

获取容器的PID
```
$ docker inspect --format "{{.State.Pid}}" <container_id>
```

删除一个运行中的容器
```
$ docker rm <container_id>
```

导出容器到 test.tar 文件
```
$ docker export <container_id> > test.tar
```

从 test.tar 文件导入，成为镜像
```
$ cat test.tar | docker import - test:v1.0
```

挂载本地主机的目录到容器内
```
$ docker run -d -P -v /opt/mysqldb:/var/lib/mysql mysql
```

启动 MongoDB
```
$ docker run -d -p 27017:27017 -e AUTH=no --name MongoDB mongo
```

启动 ElasticSearch
```
$ docker run -d -p 9200:9200 -p 9300:9300 --name ElasticSearch elasticsearch
```

## Docker Compose
测试安装结果
```
$ docker-compose --version
```

自动构建镜像并使用镜像在后台启动容器
```
$ docker-compose up -d
```

查看 docker-compose build 的帮助
```
$ docker-compose help build
```

查看服务的日志输出
```
$ docker-compose logs
```

列出所有容器
```
$ docker-compose ps
```

启动指定服务已存在的容器
```
$ docker-compose start 服务名称
```

停止已运行的容器
```
$ docker-compose stop 服务名称
```

删除指定服务的容器
```
$ docker-compose rm 服务名称
```

## 其他
获取容器的输出信息
```
$ docker logs <container_id>
```
