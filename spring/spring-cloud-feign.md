# Spring Cloud Feign

## 服务消费者整合 Feign
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
</dependency>
```

FeignClient.java
```java
import org.springframework.cloud.netflix.feign.FeignClient;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@FeignClient(name = "客户端名称")
public interface FeignClient
{
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public Object findById(@PathVariable("id") Long id);
}
```

Controller.java
```java
@RestController
public class Controller
{
    @Autowired
    private FeignClient feignClient;

    @GetMapping("/{id}")
    public Object findById(@PathVariable Long id)
    {
        return this.feignClient.findById(id);
    }
}
```

Application.java
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.netflix.feign.EnableFeignClients;

@EnableDiscoveryClient
@SpringBootApplication
@EnableFeignClients
public class Application
{
    public static void main(String[] args)
    {
        SpringApplication.run(Application.class, args);
    }
}
```

## 自定义 Feign 的配置，使用 Feign 自带的注解进行工作
FeignConfiguration.java
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import feign.Contract;

@Configuration
public class FeignConfiguration
{
    @Bean
    public Contract feignContract()
    {
        return new feign.Contract.Default();
    }
}
```

FeignClient.java
```java
import org.springframework.cloud.netflix.feign.FeignClient;

import feign.Param;
import feign.RequestLine;

@FeignClient(name = "客户端名称", configuration = FeignConfiguration.class)
public interface FeignClient
{
    @RequestLine("GET /{id}")
    public Object findById(@Param("id") Long id);
}
```
