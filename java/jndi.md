# JNDI 是什么
JNDI 是 J2EE 的标准之一，目的是消除程序与目录系统之间的耦合，使程序可配置并且高可扩展。

# 使用 Spring Boot Embedded Tomcat 配置 JNDI 连接 MySQL

pom.xml 主要配置
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.6.RELEASE</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jdbc</artifactId>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
    </dependency>
</dependencies>

<properties>
    <java.version>1.8</java.version>
</properties>
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

JNDIConfig.java
```java
import org.apache.catalina.Context;
import org.apache.catalina.startup.Tomcat;
import org.apache.tomcat.util.descriptor.web.ContextResource;
import org.springframework.boot.context.embedded.tomcat.TomcatEmbeddedServletContainer;
import org.springframework.boot.context.embedded.tomcat.TomcatEmbeddedServletContainerFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jndi.JndiObjectFactoryBean;

import javax.naming.NamingException;
import javax.sql.DataSource;

@Configuration
public class JNDIConfig
{
    @Bean
    public TomcatEmbeddedServletContainerFactory tomcatFactory()
    {
        return new TomcatEmbeddedServletContainerFactory()
        {
            @Override
            protected TomcatEmbeddedServletContainer getTomcatEmbeddedServletContainer(Tomcat tomcat)
            {
                tomcat.enableNaming();
                return super.getTomcatEmbeddedServletContainer(tomcat);
            }

            @Override
            protected void postProcessContext(Context context)
            {
                ContextResource resource = new ContextResource();

                resource.setType(DataSource.class.getName());
                resource.setName("jndi-mysql");
                resource.setProperty("factory", "org.apache.tomcat.jdbc.pool.DataSourceFactory");
                resource.setProperty("driverClassName", "com.mysql.jdbc.Driver");
                resource.setProperty("url", "jdbc:mysql://localhost:3306/xxx");
                resource.setProperty("username", "root");
                resource.setProperty("password", "root");

                context.getNamingResources().addResource(resource);
            }
        };
    }

    @Bean
    public DataSource jndiDataSource() throws IllegalArgumentException, NamingException
    {
        JndiObjectFactoryBean bean = new JndiObjectFactoryBean();
        bean.setJndiName("java:/comp/env/jndi-mysql");
        bean.setProxyInterface(DataSource.class);
        bean.setLookupOnStartup(false);
        bean.afterPropertiesSet();

        return (DataSource) bean.getObject();
    }
}
```

JNDIController.java
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import java.util.List;
import java.util.Map;

@RestController
@RequestMapping("/jndi")
public class JNDIController
{
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @PostMapping("/mysql")
    @ResponseBody
    public void mysql()
    {
        List<Map<String, Object>> rows = jdbcTemplate.queryForList("SELECT * FROM xxx");
        rows.forEach(m -> m.values().forEach(System.out::println));
    }
}
```

# 参考
[Spring Boot Configure DataSource Using JNDI with Example](https://www.java4s.com/spring-boot-tutorials/spring-boot-configure-datasource-using-jndi-with-example/)
