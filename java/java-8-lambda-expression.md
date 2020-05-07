# Java 8 Lambda 表达式

## 不需要声明参数类型

Person.java
```java
public interface Person
{
    void say(String message);
}
```

Calculator.java
```java
public interface Calculator
{
    int calculate(int a, int b);
}
```

Main.java
```java
public class Main
{
    public static void main(String[] args)
    {
        Person person = message -> System.out.println(message);
        person.say("Hello world");
        
        Calculator add = (a, b) -> a + b;
        Calculator subtract = (a, b) -> a - b;
        Calculator multiply = (a, b) -> a * b;
        Calculator divide = (a, b) -> a / b;
        System.out.println(add.calculate(10, 5));
        System.out.println(subtract.calculate(10, 5));
        System.out.println(multiply.calculate(10, 5));
        System.out.println(divide.calculate(10, 5));
    }
}
```

## 常用

Person 列表按照主键 id 分组
```java
List<Person> list = Lists.newArrayList();
...
Map<String, Person> map = list.stream().collect(Collectors.toMap(Person::getId, Function.identity))
```

Person 列表按照年龄 age 分组
```java
List<Person> list = Lists.newArrayList();
...
Map<Integer, List<Person>> map = list.stream().collect(Collectors.groupingBy(Person::getAge))
```

## 参考
[Java 8 Lambda 表达式](https://www.runoob.com/java/java8-lambda-expressions.html)  
