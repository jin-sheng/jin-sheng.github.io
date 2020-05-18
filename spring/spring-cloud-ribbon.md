# Spring Cloud Ribbon

pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-ribbon</artifactId>
</dependency>
```

@LoadBalanced 注解
```java
@Bean
@LoadBalanced
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

## 客户端负载平衡器 
注入客户端负载平衡器
```java
@Autowired
private LoadBalancerClient loadBalancerClient;
```

使用 API 直观地获取当前选择的微服务节点
```java
ServiceInstance serviceInstance = this.loadBalancerClient.choose("虚拟主机名");
logger.info("{}:{}:{}", serviceInstance.getServiceId(), serviceInstance.getHost(), serviceInstance.getPort());
```

## 自定义 Ribbon 的负载均衡策略

创建 Ribbon 的配置类
```java
@Configuration
public class RibbonConfiguration {
    @Bean
    public IRule ribbonRule() {
        // 负载均衡规则，改为随机
        return new RandomRule();
    }
}
```

@RibbonClient 注解
```java
@Configuration
@RibbonClient(name = "虚拟主机名", configuration = RibbonConfiguration.class)
public class RibbonConfiguration {}
```

## 使用属性自定义 Ribbon 的负载均衡策略

application.yml
```yml
虚拟主机名:
  ribbon:
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule
```

## 脱离 Eureka 使用 Ribbon
application.yml
```yml
虚拟主机名:
  ribbon:
    listOfServers: localhost:8000,localhost:8001
```
