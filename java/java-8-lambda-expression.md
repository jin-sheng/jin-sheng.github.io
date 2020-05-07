# Java 8 Lambda 表达式

## 示例

Person.java
```java
public interface Person
{
    void say(String message);
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
    }
}
```

## 示例

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

## 参考
[Java 8 Lambda 表达式](https://www.runoob.com/java/java8-lambda-expressions.html)  
