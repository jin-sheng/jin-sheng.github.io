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

Git 仓库中创建配置文件
```
spring-cloud-sample-dev.properties
```

禁用健康状况指示器
```properties
spring.cloud.config.server.health.enabled=false
```

## Config Client

pom.xml
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Application.java
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
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
  port: 8081
```

bootstrap.yml
```yml
spring:
  application:
    name: spring-cloud-sample
  cloud:
    config:
      uri: http://localhost:8080/
      profile: dev
      label: master
```

## 使用 /refresh 端点手动刷新配置

pom.xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Controller.java
```java
@RestController
@RefreshScope
public class Controller
{
    ...
}
```

发送 POST 请求
```shell
$ curl -X POST http://localhost:8081/refresh
```
