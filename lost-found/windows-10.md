# Windows 10

查看所有端口
```bash
# netstat -ano
```

查看指定端口
```bash
# netstat -aon | findstr 8080
```

查看指定端口占用
```bash
# tasklist | findstr 8080
```
