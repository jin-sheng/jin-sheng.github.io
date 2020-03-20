# 点评 CAT Docker 快速部署（Windows 环境）
## Github

https://github.com/dianping/cat
<br>
https://github.com/dianping/cat/wiki/readme_server#2-docker快速部署

## Docker

安装 Docker Desktop Community
```url
https://www.runoob.com/docker/windows-docker-install.html
```

开启本地或远程 API 调用
```
Settings -> General -> 勾选 Expose daemon on tcp://localhost:2375 without TLS
```
配置 Docker Engine
```json
{
  "registry-mirrors": [
    "https://registry.docker-cn.com"
  ],
  "insecure-registries": [],
  "debug": true,
  "experimental": false,
  "host": [
    "tcp://0.0.0.0:2375"
  ]
}
```
## Git Bash

克隆

```bash
$ git config --global core.autocrlf false # windows 环境必须执行，否则 cat 实例可能无法启动
$ git clone https://github.com/dianping/cat.git
```
修改 dianping/cat/docker/docker-compose.yml
```yml
# 替换 volumes
volumes:
    # - "./client.xml:/data/appdatas/cat/client.xml"
    - "/d/Workspaces/GitHub/dianping/cat/docker/client.xml:/data/appdatas/cat/client.xml"
    # - "./mysql/volume:/var/lib/mysql"
    - "/d/Workspaces/GitHub/dianping/cat/docker/mysql/volume:/var/lib/mysql"
    # - "../script/CatApplication.sql:/init.sql"
    - "/d/Workspaces/GitHub/dianping/cat/script/CatApplication.sql:/init.sql"

# 注释 links
#    links:
#      - mysql

# 注释 network_mode
#    network_mode: "host"    
```

运行
```docker
docker-compose up
```
初始化 MySQL
```docker
docker exec <container_id> bash -c "mysql -uroot -Dcat < /init.sql"
```
访问
```url
http://127.0.0.1:8080/cat
```

## FAQ

- [docker-compose start kibana failed!--No such file or directory/usr/bin/env: bash #36](https://github.com/deviantony/docker-elk/issues/36) 
- [docker-compose up -d doesn't expose ports when defined with build directive #4799](https://github.com/docker/compose/issues/4799)
