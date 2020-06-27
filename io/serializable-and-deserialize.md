# 序列化与反序列化

序列化：把对象转换为字节序列的过程。  
反序列化：把字节序列恢复为对象的过程。

## 使用场景
对内存中的对象进行持久化。  
网络传输。

## 实现方式
实现 java.io.Serializable 接口。  
自行编码实现。

## 为什么没有实现 java.io.Serializable 接口也能进行持久化或网络传输？
java.lang.String 类实现了 java.io.Serializable 接口，并显示指定 serialVersionUID 的值。

## 不能被序列化的情况
被 transient 关键字修饰的属性不会被序列化。  
被 static 关键字修饰的属性不会被序列化。

## 参考
[序列化和反序列化](https://mp.weixin.qq.com/s/KgyvDQ_kNwmqp2duqtkFBA)  
