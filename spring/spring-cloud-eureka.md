# 服务发现组件 Eureka

## Eureka Server
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka-server</artifactId>
</dependency>
```

## 将微服务注册到 Eureka Server 上
pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

application.yml
```yml
spring:
  application:
    name: spring-cloud-sample
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
public class Application
{
    public static void main(String[] args)
    {
        SpringApplication.run(Application.class, args);
    }
}
```

## Eureka Server 集群
/etc/hosts
```hosts
127.0.0.1 peer1 peer2
```

application.yml
```yml
spring:
  application:
    name: spring-cloud-sample
---
spring:
  profiles: peer1                                 # 指定profile=peer1
server:
  port: 8761
eureka:
  instance:
    hostname: peer1                               # 指定当profile=peer1时，主机名是peer1
  client:
    serviceUrl:
      defaultZone: http://peer2:8762/eureka/      # 将自己注册到peer2这个Eureka上面去

---
spring:
  profiles: peer2
server:
  port: 8762
eureka:
  instance:
    hostname: peer2
  client:
    serviceUrl:
      defaultZone: http://peer1:8761/eureka/
```

启动
```shell
$ java -jar spring-cloud-sample-0.0.1-SNAPSHOT --spring.profiles.active=peer1
$ java -jar spring-cloud-sample-0.0.1-SNAPSHOT --spring.profiles.active=peer2
```

## 将微服务注册到 Eureka Server 集群上

application.yml
```yml
eureka:
  client:
    serviceUrl:
      defaultZone: http://peer1:8761/eureka/,http://peer2:8762/eureka/
```

## 需认证的 Eureka Server

pom.xml
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

application.yml
```yml
security:
  basic:
    enabled: true               # 开启基于HTTP basic的认证
  user:
    name: user                  # 配置登录的账号是user
    password: password123       # 配置登录的密码是password123
```

## 将微服务注册到需认证的 Eureka Server 集群上

application.yml
```yml
eureka:
  client:
    serviceUrl:
      defaultZone: http://user:password123@localhost:8761/eureka/
```

## 使用 REST 端点将微服务注册到 Eureka Server 上

符合 XSD 的 XML 文件 rest-api-test.xml
```xml
<instance>
    <instanceId>spring-cloud-sample:rest-api-test:9000</instanceId>
    <hostName>itmuch</hostName>
    <app>REST-API-TEST</app>
    <ipAddr>127.0.0.1</ipAddr>
    <vipAddress>rest-api-test</vipAddress>
    <secureVipAddress>rest-api-test</secureVipAddress>
    <status>UP</status>
    <port enabled="true">9000</port>
    <securePort enabled="false">443</securePort>
    <homePageUrl>http://127.0.0.1:9000/</homePageUrl>
    <statusPageUrl>http://127.0.0.1:9000/info</statusPageUrl>
    <healthCheckUrl>http://127.0.0.1:9000/health</healthCheckUrl>
    <dataCenterInfo class="com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo">
        <name>spring-cloud-sample</name>
    </dataCenterInfo>
</instance>
```

使用 curl 命令
```shell
$ cat ./rest-api-test.xml | curl -v -X POST -H "Content-type: application/xml" -d @- http://localhost:8761/eureka/apps/rest-api-test
```

查看微服务 rest-api-test 的所有实例
```url
http://localhost:8761/eureka/apps/rest-api-test
```

## 参考
[Spring Cloud 与 Docker 微服务架构实战](https://github.com/itmuch/spring-cloud-docker-microservice-book-code)  
