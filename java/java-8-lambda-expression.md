# Java 8 Lambda 表达式

## 语法
```
(argument) -> (body)
```

## 函数式接口

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

启动一个线程
```java
new Thread(
    () -> System.out.println("Hello world")
).start();
```

Person 列表按照主键 id 分组
```java
Map<String, Person> map = personList.stream().collect(Collectors.toMap(Person::getId, Function.identity));
```

Person 列表按照年龄 age 分组
```java
Map<Integer, List<Person>> map = personList.stream().collect(Collectors.groupingBy(Person::getAge));
```

打印所有 Person 的 name
```java
personList..forEach(person -> System.out.println(person.getName()));
```

求平方
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
list.stream().map((x) -> x * x).forEach(System.out::println);
```

求平方和
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
int sum = list.stream().map(x -> x * x).reduce((x, y) -> x + y).get();
System.out.println(sum);
```

## 参考
[Java 8 Lambda 表达式](https://www.runoob.com/java/java8-lambda-expressions.html)  
