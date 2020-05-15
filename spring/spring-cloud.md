# Spring Cloud

## 服务监控组件 Actuator
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

## 服务发现组件 Eureka
### Eureka Server
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka-server</artifactId>
</dependency>
```

### 将微服务注册到 Eureka Server 上
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

application.yml
```yml
...
eureka:
  client:
    serviceUrl:
      defaultZone: http://[ip]:[port]/eureka/
  instance:
    prefer-ip-address: true
```

Application.java
```java
@EnableDiscoveryClient
@SpringBootApplication
public class ProviderUserApplication
{
    public static void main(String[] args)
    {
        SpringApplication.run(ProviderUserApplication.class, args);
    }
}
```

## 参考
[Spring Cloud 与 Docker 微服务架构实战]()  
