# Spring Cloud Hystrix

## 服务消费者整合 Hystrix
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-actuator</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
</dependency>
```

Application.java
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.hystrix.EnableHystrix;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@EnableDiscoveryClient
@SpringBootApplication
@EnableHystrix
public class Application
{
    public static void main(String[] args)
    {
        SpringApplication.run(Application.class, args);
    }
}
```

@HystrixCommand 注解
```java
@HystrixCommand(fallbackMethod = "xxx")
@GetMapping("/user/{id}")
public User findById(@PathVariable Long id)
{
    ...
}
```

## 指定隔离策略（默认THREAD）
application.properties
```properties
execution.isolation.strategy=SEMAPHORE
```
