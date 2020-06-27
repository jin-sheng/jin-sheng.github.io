# Java 泛型

## 什么是泛型
能够让代码不拘泥于具体的类型，而是应用于多种类型。

## 如何使用泛型
泛型接口
```java
public interface DemoService<T>
{
    ...
}
```

泛型类
```java
public class DemoServiceImpl<T> extends DemoService<T>
{
    ...
}
```

泛型方法
```java
public <T> T getById(String id)
{
    ...
}
```

## 泛型能带来什么好处

||代码可读性|代码复用性|强制类型转换|发现错误的时机|
|---|---|---|---|---|
|不使用泛型|较差|较低|必须|运行阶段|
|使用泛型|较好|较高|非必须|编译阶段|

### 代码可读性、代码复用性
不使用泛型
```java
public interface Service
{
    A getByAid(String aid);
    B getByBid(String bid);
    C getByCid(String cid);
}
```

使用泛型
```java
public interface Service<T>
{
    T getById(String id);
}
```

### 强制类型转换、发现错误的时机
不使用泛型
```java
List list = new ArrayList();
list.add(123);
String s = (String) list.get(0); // 运行时抛出 java.lang.ClassCastException 异常
```

使用泛型
```java
List<String> list = new ArrayList<>();
list.add("123");
// int i = list.get(0); // 编译时报错
String s = list.get(0); // 不用强制类型转换
```



## 泛型擦除
