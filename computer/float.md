# 浮点数

## IEEE754标准
二进制浮点运算标准，大大改善了应用程序的可移植性。

## 浮点数的表现形式
```
(-1)^s x m x n^e

# s 符号，0 代表正数，1 代表负数
# m 尾数
# n 基数
# e 指数
```

## 十进制小数转换成二进制浮点数格式
步骤
- 将整数部分转换成二进制
- 将小数部分转换成二进制
- 得到完整的二进制小数
- 将二进制小数标准化得到二进制浮点数
- 得到符号位（0：正数，1：负数）
- 得到指数位（单精度：8位指数，双精度：11位指数，左补零）
- 得到尾数位（单精度：23位尾数，双精度：52位尾数，右补零）
- 得到二进制浮点数格式

举例：十进制的 10.625 转换成二进制的单精度浮点数
- 将整数部分转换成二进制：除 2 取余法，10/2=5余0，5/2=2余1，2/2=1余0，1/2=0余1，1010
- 将小数部分转换成二进制：乘 2 取整法，0.625x2=1.25，0.25x2=0.5，0.5x2=1.0，101
- 得到完整的二进制小数：1010.101
- 将二进制小数标准化得到二进制浮点数：1.010101 x 2^-3
- 得到符号位：0
- 得到指数位：移动位数 + 偏移量 = 3 + 127 = 130，转换成二进制=10000010
- 得到尾数位：01010100000000000000000
- 得到二进制浮点数格式：0-10000010-01010100000000000000000，即 01000001001010100000000000000000，表示为十六进制为 0x412A0000

举例：十进制的 10.625 转换成二进制的双精度浮点数
- 将整数部分转换成二进制：除 2 取余法，10/2=5余0，5/2=2余1，2/2=1余0，1/2=0余1，1010
- 将小数部分转换成二进制：乘 2 取整法，0.625x2=1.25，0.25x2=0.5，0.5x2=1.0，101
- 得到完整的二进制小数：1010.101
- 将二进制小数标准化得到二进制浮点数：1.010101 x 2^-3
- 得到符号位：0
- 得到指数位：移动位数 + 偏移量 = 3 + 1023 = 1026，转换成二进制=10000000010
- 得到尾数位：0101010000000000000000000000000000000000000000000000
- 得到二进制浮点数格式：0-10000000010-0101010000000000000000000000000000000000000000000000，即 0100000000100101010000000000000000000000000000000000000000000000，表示为十六进制为 0x4025400000000000

## 二进制浮点数格式转换成十进制小数
步骤
- 得到符号位
- 得到尾数位
- 得到指数位
- 将指数位转换成指数
- 将尾数位转换成尾数
- 通过公式【(-1) ^ 符号 x (1 + 尾数) x 2 ^ (指数 - 127)】计算十进制小数

举例：二进制的单精度浮点数格式 01000001001010100000000000000000 转换成十进制小数 10.625
- 得到符号位：0
- 得到指数位：10000010
- 得到尾数位：01010100000000000000000
- 将指数位转换成指数：指数 = 2^7 + 2^1 = 130
- 将尾数位转换成尾数：尾数 = 2^-2 + 2^-4 + 2^-6 = 0.328125
- 通过公式【(-1) ^ 符号 x (1 + 尾数) x 2 ^ (指数 - 偏移量)】计算十进制小数：(-1) ^ 0 x (1 + 0.328125) x 2 ^ (130 - 127) = 10.625

举例：二进制的双精度浮点数格式 0100000000100101010000000000000000000000000000000000000000000000 转换成十进制小数 10.625
- 得到符号位：0
- 得到指数位：10000000010
- 得到尾数位：0101010000000000000000000000000000000000000000000000
- 将指数位转换成指数：指数 = 2^10 + 2^1 = 1026
- 将尾数位转换成尾数：尾数 = 2^-2 + 2^-4 + 2^-6 = 0.328125
- 通过公式【(-1) ^ 符号 x (1 + 尾数) x 2 ^ (指数 - 偏移量)】计算十进制小数：(-1) ^ 0 x (1 + 0.328125) x 2 ^ (1026 - 1023) = 10.625

## 获取十进制小数的二进制浮点数格式
Java
```java
// 单精度浮点数
float f = 0.75f;
int i = Float.floatToIntBits(f);
System.out.println(Integer.toBinaryString(i));

// 双精度浮点数
double d = 10.625d;
long l = Double.doubleToLongBits(d);
System.out.println(Long.toBinaryString(l));
```

## 参考
[《Java开发手册》解读：大整数传输为何禁用Long类型?](https://mp.weixin.qq.com/s?__biz=MzIzOTU0NTQ0MA==&mid=2247498496&idx=1&sn=a46cd5d34f9afca3f31121fb3ac835e0)  
[【算法】解析IEEE 754 标准](https://www.cnblogs.com/HDK2016/p/10506083.html)  
[binaryconvert](https://www.binaryconvert.com/index.html)  
[浮点数，你真的懂了吗？](https://mp.weixin.qq.com/s/vHxqOESLdEutvfsjbGRtQQ)  
