# Spring Validation

## 验证框架的种类

|注解|框架|规范|支持分组|支持嵌套|
|---|---|---|---|---|
|@Valid|javax|标准 JSR-303|不支持|支持|
|@Validation|springframework|标准 JSR-303 的变种|支持|需配合 @Valid|

## 嵌套验证
Student.java
```java
import javax.validation.constraints.Min;
import javax.validation.constraints.NotEmpty;
import javax.validation.constraints.NotNull;

public class Student
{
    @NotEmpty(message = "姓名不能为空")
    private String name;

    @NotNull(message = "年龄不能为空")
    @Min(value = 6, message = "年龄最小6岁")
    private Integer age;

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

School.java
```java
import javax.validation.Valid;
import javax.validation.constraints.NotEmpty;
import java.util.List;

public class School
{
    @NotEmpty(message = "学校名称不能为空")
    private String name;

    @Valid
    @NotEmpty(message = "学生不能为空")
    private List<Student> studentList;

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public List<Student> getStudentList()
    {
        return studentList;
    }

    public void setStudentList(List<Student> studentList)
    {
        this.studentList = studentList;
    }
}
```

Controller.java
```java
import org.springframework.validation.BindingResult;
import org.springframework.validation.ObjectError;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class Controller
{
    @PostMapping("/school/add")
    public void add(@Validated @RequestBody School school, BindingResult result)
    {
        ...
    }
}
```
或
```java
import org.springframework.validation.BindingResult;
import org.springframework.validation.ObjectError;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import javax.validation.Valid;

@RestController
public class Controller
{
    @PostMapping("/school/add")
    public void add(@Valid @RequestBody School school, BindingResult result)
    {
        ...
    }
}
```
