# 箭头函数

条件运算
```javascript
var simple = a => a > 15 ? 15 : a;
simple(16); // 15
simple(10); // 10

let max = (a, b) => a > b ? a : b;
```

递归
```javascript
var fact = (x) => ( x==0 ?  1 : x*fact(x-1) );
fact(5);       // 120
```
