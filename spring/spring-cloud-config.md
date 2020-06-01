# Spring Cloud Config

## Config Server

pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

Application.java
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.config.server.EnableConfigServer;

@SpringBootApplication
@EnableConfigServer
public class Application
{
    public static void main(String[] args)
    {
        SpringApplication.run(Application.class, args);
    }
}
```

application.yml
```yml
server:
  port: 8080
spring:
  application:
    name: 微服务名称
  cloud:
    config:
      server:
        git:
          uri: Git仓库的地址
          username: Git仓库的账号
          password: Git仓库的密码
```
