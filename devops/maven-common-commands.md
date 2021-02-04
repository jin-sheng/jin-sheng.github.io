# Maven 常用命令

查看依赖树
```bash
$ mvn dependency:tree
```

clean install 跳过测试并指定本地 setting.xml 文件
```bash
$ mvn clean install -Dmaven.test.skip=true -s /path/to/settings.xml
```
