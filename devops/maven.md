# Maven
## settings.xml
配置阿里云镜像
```xml
<!-- 在 mirrors 节点中配置如下 -->
<mirror>
  <id>alimaven</id>
  <name>aliyun maven</name>
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
  <mirrorOf>central</mirrorOf>
</mirror>
```

## IDEA 插件
生成 IntelliJ IDEA 项目使用的文件
```shell
$ mvn idea:idea
```

删除 IntelliJ IDEA 项目使用的文件
```shell
$ mvn idea:clean
```

生成 ipr 文件
```shell
$ mvn idea:project
```

生成 iml 文件
```shell
$ mvn idea:module
```

生成 iws 文件
```shell
$ mvn idea:workspace
```

# 参考
[Apache Maven IDEA Plugin (RETIRED)](http://maven.apache.org/plugins/maven-idea-plugin/)
