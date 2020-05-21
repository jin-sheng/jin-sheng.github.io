# Spring Cloud Zuul

## 指定 Zuul 使用 RestClient 作为 HTTP 客户端
```propertiess
ribbon.restclient.enabled=true
```

## 指定 Zuul 使用 okhttp3.OkHttpClient 作为 HTTP 客户端
```propertiess
ribbon.okhttp.enabled=true
```

## Zuul 微服务网关
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zuul</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

Application.java
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.zuul.EnableZuulProxy;

@SpringBootApplication
@EnableZuulProxy
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
  port: 8040
spring:
  application:
    name: 微服务名称
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

## Zuul 路由配置
将微服务映射到 /user/** 路径
```yml
zuul:
  routes:
    微服务名称: /user/**
```

忽略指定微服务
```yml
zuul:
  ignored-services: 微服务1,微服务2
```

忽略所有微服务，只路由指定微服务
```yml
zuul:
  ignored-services: '*'
  routes:
    微服务名称: /user/**
```

将微服务映射到 /user/** 路径，但忽略该微服务中所有包含 /admin/ 的路径
```yml
zuul:
  ignoredPatterns: /**/admin/**
  routes:
    微服务名称: /user/**
```
