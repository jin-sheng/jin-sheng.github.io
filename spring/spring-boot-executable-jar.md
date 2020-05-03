# Spring Boot 可执行 jar

## 快速启动
pom.xml
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

com.example.demo.DemoApplication
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication
{
    public static void main(String[] args)
    {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

打包
```shell
$ mvn package
```

运行
```shell
$ java -jar spring-boot-demo.jar
```

## 过程解析

target/demo-0.0.1-SNAPSHOT.jar.original（maven repackage 前的原始 jar）/META-INF/MANIFEST.MF
```
Manifest-Version: 1.0
Created-By: Maven Archiver 3.4.0
Build-Jdk-Spec: 1.8
Implementation-Title: demo
Implementation-Version: 0.0.1-SNAPSHOT
```

target/demo-0.0.1-SNAPSHOT.jar（maven repackage 后的可执行 jar）/META-INF/MANIFEST.MF
```
Manifest-Version: 1.0
Created-By: Maven Archiver 3.4.0
Build-Jdk-Spec: 1.8
Implementation-Title: demo
Implementation-Version: 0.0.1-SNAPSHOT
Main-Class: org.springframework.boot.loader.JarLauncher
Start-Class: com.example.demo.DemoApplication
Spring-Boot-Version: 2.2.6.RELEASE
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/li
```

## 参考
[为什么SpringBoot的 jar 可以直接运行？](https://mp.weixin.qq.com/s?__biz=MzA4NjgxMjQ5Mg==&mid=2665763886&idx=1&sn=70a5ec87f91aa00709925b9d267838f4)  
