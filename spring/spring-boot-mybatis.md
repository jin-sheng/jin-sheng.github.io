# Spring Boot 集成 MyBatis

建库建表
```sql
CREATE DATABASE mybatis CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE TABLE USER ( 
  id int(11) not null AUTO_INCREMENT,
  name varchar(20) not null,
  age smallint not null,
  PRIMARY KEY (id) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

pom.xml
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.3</version>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

application.properties
```properties
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/mybatis?useUnicode=true&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

User.java
```java
public class User
{
    private Long id;
    private String name;
    private Integer age;

    public Long getId()
    {
        return id;
    }

    public void setId(Long id)
    {
        this.id = id;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public Integer getAge()
    {
        return age;
    }

    public void setAge(Integer age)
    {
        this.age = age;
    }
}
```

UserMapper.java
```java
import org.apache.ibatis.annotations.*;
import java.util.List;

@Mapper
public interface UserMapper
{
    @Insert("insert into user(name,age) values(#{name},#{age})")
    @Options(useGeneratedKeys = true, keyColumn = "id", keyProperty = "id")
    Long insert(User user);

    @Update("update user set name=#{name},age=#{age} where id=#{id}")
    Long update(User user);

    @Delete("delete from user where id=#{id}")
    Long delete(@Param("id") Long id);

    @Select("select id,name,age from user")
    List<User> selectAll();

    @Select("select id,name,age from user where id=#{id}")
    User selectById(@Param("id") Long id);
}
```

UserController.java
```java
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class UserController
{
    @Autowired
    private SqlSessionFactory sqlSessionFactory;

    @GetMapping("/save")
    public Long save(@RequestParam String name, @RequestParam int age)
    {
        try (SqlSession session = sqlSessionFactory.openSession())
        {
            UserMapper userMapper = session.getMapper(UserMapper.class);
            User user = new User();
            user.setName(name);
            user.setAge(age);
            userMapper.insert(user);
            return user.getId();
        }
    }

    @GetMapping("/update/{id}")
    public Long update(@PathVariable Long id, @RequestParam String name, @RequestParam int age)
    {
        try (SqlSession session = sqlSessionFactory.openSession())
        {
            UserMapper userMapper = session.getMapper(UserMapper.class);
            User user = new User();
            user.setId(id);
            user.setName(name);
            user.setAge(age);
            return userMapper.update(user);
        }
    }

    @GetMapping("/delete/{id}")
    public Long save(@PathVariable Long id)
    {
        try (SqlSession session = sqlSessionFactory.openSession())
        {
            UserMapper userMapper = session.getMapper(UserMapper.class);
            return userMapper.delete(id);
        }
    }

    @GetMapping("/list")
    public List<User> list()
    {
        try (SqlSession session = sqlSessionFactory.openSession())
        {
            UserMapper userMapper = session.getMapper(UserMapper.class);
            return userMapper.selectAll();
        }
    }

    @GetMapping("/get/{id}")
    public User get(@PathVariable Long id)
    {
        try (SqlSession session = sqlSessionFactory.openSession())
        {
            UserMapper userMapper = session.getMapper(UserMapper.class);
            return userMapper.selectById(id);
        }
    }
}
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

## 参考
[Spring Boot + MyBatis + MySQL 整合](https://www.jianshu.com/p/c2444ddd2de9)  
