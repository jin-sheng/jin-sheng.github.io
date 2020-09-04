# 浮点数
浮点数的表现形式
```
± m x n^e

# ± 符号
# m 尾数
# n 基数
# e 指数
```

用单精度浮点数表示十进制数 0.75
```java
public static void main(String[] args)
{
    float f = 0.75f;
    int i = Float.floatToIntBits(f);
    StringBuilder sb = new StringBuilder(Integer.toBinaryString(i));
    for (int j = 32 - sb.length(); j > 0; j--)
    {
        sb.insert(0, "0");
    }
    char[] b = sb.toString().toCharArray();
    char[] c = new char[34];
    for (int j = 0, k = 0; j < 34; j++)
    {
        if (j == 1 || j == 10)
        {
            c[j] = '-';
        }
        else
        {
            c[j] = b[k];
            k++;
        }
    }
    System.out.println(c);
}
```

结果（小数部分用二进制表示=.11，正规化后=1.1x10^-1）
```
0-01111110-10000000000000000000000
```

得到符号部分
```
0
```

得到指数部分（指数=-1，单精度偏移量=127，指数部分=-1+127=126）
```
01111110
```

得到尾数部分
```
10000000000000000000000
```

根据 EXCESS 系统表现得到指数 e
```
e = 01111110 的十进制数 - 127 = 126 - 127 = -1
```

根据正则表达式得到尾数 m
```
m = 尾数部分 10000000000000000000000 实际上表示的二进制数转换成十进制数
  = 1.10000000000000000000000 转换成十进制数
  = (1x2的0次幂)+(1x2的-1次幂)
  = 1.5
```

得到十进制数 0.75
```
± m x n^e = + 1.5 x 2^-1
          = + 0.75
```

## 参考
[《Java开发手册》解读：大整数传输为何禁用Long类型?](https://mp.weixin.qq.com/s?__biz=MzIzOTU0NTQ0MA==&mid=2247498496&idx=1&sn=a46cd5d34f9afca3f31121fb3ac835e0)  
[【算法】解析IEEE 754 标准](https://www.cnblogs.com/HDK2016/p/10506083.html)
