# 适配器模式

## 意图
Adapter 模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。

## 示例
需要将 MacBook Pro 显示屏上的内容镜像输出至支持 HDMI 的电视或显示器，MacBook Pro 只具备雷雳 3 接口。

## 参与者
Target（HDMI 接口）
```java
public interface HDMI
{
    String trans();
}
```

Adaptee（USB C 接口）
```java
public class USBC
{
    private String message;

    USBC(String message)
    {
        this.message = message;
    }

    public String transUSBC()
    {
        return "USBC" + message;
    }
}
```

类适配器 Adapter（USB-C 数字影音多端口转换器）
```java
public class Adapter extends USBC implements HDMI
{
    public Adapter(String message)
    {
        super(message);
    }

    @Override
    public String trans()
    {
        String result = transUSBC();
        return this.convertUSBCToHDMI(result);
    }

    private String convertUSBCToHDMI(String message)
    {
        return "HDMI" + message;
    }
}
```

对象适配器 Adapter（USB-C 数字影音多端口转换器）
```java
public class Adapter implements HDMI
{
    private USBC usbc;
    
    public Adapter(String message)
    {
        this.usbc = new USBC(message);
    }

    @Override
    public String trans()
    {
        String result = usbc.transUSBC();
        return this.convertUSBCToHDMI(result);
    }

    private String convertUSBCToHDMI(String message)
    {
        return "HDMI" + message;
    }
}
```
