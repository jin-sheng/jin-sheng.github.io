# Maven
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
