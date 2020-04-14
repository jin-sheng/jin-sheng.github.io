# Visual VM
## 设置远程监控
在需要监控的服务器上创建 policy 文件
```shell
# vi /ux/security/visualvm.remote.policy
```

```shell
grant codebase "file:${java.home}/../lib/tools.jar" {
    permission java.security.AllPermission;
}
```

运行 jstatd 工具
```shell
# jstatd -J-Djava.security.policy=/ux/security/visualvm.remote.policy -p 9000
```
