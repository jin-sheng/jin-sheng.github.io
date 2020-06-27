# Java 泛型

## 什么是泛型
泛型即代码泛化，能够让代码不拘泥于具体的类型，而是应用于多种类型。

## 何时使用泛型
当你希望代码能够跨越多个类工作时，使用泛型才有所帮助。

## 如何使用泛型
泛型接口
```java
public interface Service<T>
{
    ...
}
```

泛型类
```java
public abstract class AbstractServiceImpl<T> implements Service<T>
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

## 为什么要擦除泛型
为了允许非泛型代码与泛型代码共存，使向着泛型的迁移成为可能。

## 参考
[面试官：十问泛型，你能扛住吗？](https://mp.weixin.qq.com/s/4XCXIvT1EfFeB5y4agbNEw)  
