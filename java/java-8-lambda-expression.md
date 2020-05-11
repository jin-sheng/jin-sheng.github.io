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

## Consumer 接口

```java
Consumer<String> c = System.out::println;
c.accept("Hello world");
```

## 常用

启动一个线程
```java
new Thread(
    () -> System.out.println("Hello world")
).start();
```

打印所有 Person 的 name
```java
personList.forEach(person -> System.out.println(person.getName()));
```

打印所有 Person 的 name 到一行上
```java
System.out.println(personList.stream().map(Person::getName).collect(Collectors.joining(", ")))
```

Person 列表按照主键 id 分组
```java
Map<String, Person> map = personList.stream().collect(Collectors.toMap(Person::getId, Function.identity));
```

Person 列表按照年龄 age 分组
```java
Map<Integer, List<Person>> map = personList.stream().collect(Collectors.groupingBy(Person::getAge));
```

过滤出年龄大于30岁的男性列表
```java
personList = personList.stream()
                       .filter(person -> person.age > 30)
                       .filter(person -> person.gender = "MAN")
                       .collect(Collectors.toList());
```

求平方
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
list.stream().map((x) -> x * x).forEach(System.out::println);
```

求平方和
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
System.out.println(list.stream().map(x -> x * x).reduce(Integer::sum).get());
```

计算集合元素的最大值、最小值、总和以及平均值
```java
List<Integer> primes = Arrays.asList(2, 3, 5, 7, 11, 13, 17, 19, 23, 29);
IntSummaryStatistics statistics = primes.stream().mapToInt((x) -> x).summaryStatistics();
System.out.println("Max : " + statistics.getMax());
System.out.println("Min : " + statistics.getMin());
System.out.println("Sum : " + statistics.getSum());
System.out.println("Average : " + statistics.getAverage());
```

## 参考
[Java 8 Lambda 表达式](https://www.runoob.com/java/java8-lambda-expressions.html)  
