# 红黑树

## 引理：一棵有 n 个内部结点的红黑树的高度至多为 2lg(n+1)
先证明以任一结点 x 为根的子树中至少包含 ![](http://latex.codecogs.com/gif.latex?2^{bh(x)}-1) 个内部结点。  

考虑一个高度为正值且有两个子结点的内部结点 x，每个子结点有黑高 bh(x) 或 bh(x) - 1。

利用归纳假设得出每个子结点至少有 ![](http://latex.codecogs.com/gif.latex?2^{bh(x)-1}-1) 个内部结点。  

于是，以 x 为根的子树至少包含 ![](http://latex.codecogs.com/gif.latex?(2^{bh(x)-1}-1)+(2^{bh(x)-1}-1)+1=2^{bh(x)}-1) 个内部结点，得证。  

设 h 为树的高度，根的黑高至少为 h/2。  

于是有 ![](http://latex.codecogs.com/gif.latex?n\geq2^{h/2}-1)  

把1移到不等式的左边，再对两边取对数，得到 ![](http://latex.codecogs.com/gif.latex?lg(n+1)\geq{h/2})  

即 ![](http://latex.codecogs.com/gif.latex?h\leq2lg(n+1))
