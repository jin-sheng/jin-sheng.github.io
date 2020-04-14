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

十进制数 0.75 用单精度浮点数来表示
```
0-01111110-10000000000000000000000
```

得到符号部分
```
0
```

得到指数部分
```
01111110
```

得到尾数部分
```
10000000000000000000000
```

根据 EXCESS 系统表现得到指数 e
```
e = 01111110 的十进制数 - 127 = 126 -127 = -1
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
