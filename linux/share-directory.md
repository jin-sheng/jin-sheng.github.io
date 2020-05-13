# 共享目录

## 服务端配置

通过 yum 的方式在线安装 nfs、rpcbind 服务
```shell
# yum -y install nfs-utils rpcbind
```

配置共享目录 /opt/share 并且 192.168.137 开头的 IP 都有访问权限
```shell
# echo '/data 192.168.137.0/24(rw,no_root_squash,no_all_squash,sync)' >> /etc/exports
```

配置即时生效
```shell
# exportfs -r
```

配置开机启动
```shell
# chkconfig --level 2345 rpcbind on
# chkconfig --level 2345 nfs on
```

测试共享服务是否配置正确
```shell
# showmount -e 127.0.0.1
```

## 客户端配置

通过 yum 的方式在线安装 autofs 服务
```shell
# yum -y install autofs showmount
```

检查 nfs 服务器的共享，是否给本服务器开放了权限
```shell
# showmount -e 192.168.137.6
```

创建本地挂载目录
```shell
# mkdir /opt/share
```

配置挂载配置文件 /etc/auto.master
```shell
# sed -i'$i\/- /etc/auto.nfsdata' /etc/auto.master
```

拷贝挂载规则配置文件 /etc/auto.misc 为 /etc/auto.nfsdata
```shell
# cp /etc/auto.misc /etc/auto.nfsdata
```

配置挂载规则
```shell
# sed -i '$a\/opt/share -rw,soft,intr 192.168.137.6:/opt/share' /etc/auto.nfsdata
```

重启autofs服务
```shell
# service autofs restart
```

配置服务自动启动
```shell
# chkconfig --level 2345 autofs on
```
