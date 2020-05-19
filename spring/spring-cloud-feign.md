# Spring Cloud Feign

## 服务消费者整合 Feign
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
</dependency>
```

UserFeignClient.java
```java
import org.springframework.cloud.netflix.feign.FeignClient;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@FeignClient(name = "客户端名称")
public interface UserFeignClient
{
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public User findById(@PathVariable("id") Long id);
}
```

Controller.java
```java
@RestController
public class Controller
{
    @Autowired
    private UserFeignClient userFeignClient;

    @GetMapping("/{id}")
    public User findById(@PathVariable Long id)
    {
        return this.userFeignClient.findById(id);
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

UserFeignClient.java
```java
import org.springframework.cloud.netflix.feign.FeignClient;

import feign.Param;
import feign.RequestLine;

@FeignClient(name = "客户端名称", configuration = FeignConfiguration.class)
public interface UserFeignClient
{
    @RequestLine("GET /{id}")
    public User findById(@Param("id") Long id);
}
```

## Feign 对压缩的支持
对请求或响应进行压缩
```application.properties
feign.compression.request.enabled=true
```

对响应进行压缩
```application.properties
feign.compression.response.enabled=true
```

设置支持的媒体类型列表
```application.properties
feign.compression.request.mime-types=text/xml,application/xml,application/json
```

设置请求的最小阈值
```application.properties
feign.compression.request.min-request-size=2048
```

## 使用 Feign 构造多参数请求

GET 请求多参数方法一
```java
@FeignClient(name = "客户端名称")
public interface UserFeignClient
{
    @RequestMapping(value = "/get", method = RequestMethod.GET)
    public User get(@RequestParam("id") Long id, @RequestParam("username") String username);
}
```

GET 请求多参数方法二
```java
@FeignClient(name = "客户端名称")
public interface UserFeignClient
{
    @RequestMapping(value = "/get", method = RequestMethod.GET)
    public User get(@RequestParam Map<String, Object> map);
}
```

POST 请求多参数
```java
@FeignClient(name = "客户端名称")
public interface UserFeignClient
{
    @RequestMapping(value = "/post", method = RequestMethod.POST)
    public User post(@RequestBody User user);
}
```
