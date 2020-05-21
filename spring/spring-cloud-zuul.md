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
