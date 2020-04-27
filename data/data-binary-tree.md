# 二叉树

## 种类

|种类|顺序存储|链式存储|遍历|备注|
|---|---|---|---|---|
|完全二叉树|√||O(n)||
|满二叉树|√||O(n)||
|线索二叉树||√|O(n)|按某种遍历次序进行线索化的二叉树<br>直接找到某结点在某种遍历次序下的前驱或后继结点|
|平衡二叉树||√|O(n)||
|二叉搜索树||√|O(n)|对任何结点 x<br>其左子树中的所有关键字都比 x 小<br>其右子树中的所有关键字都比 x 大|
|红黑树||√||保证在最坏情况下基本动态集合操作的时间复杂度为 O(lgn)|
|哈夫曼树||√||哈夫曼编码是一种无损压缩<br>获得哈夫曼编码的过程也就是建立哈夫曼树的过程|

## 链式存储结构

二叉链表
```java
public class BinaryNode<E>
{
    public E data;
    public BinaryNode<E> left, right;
}
```

三叉链表
```java
public class BinaryNode<E>
{
    public E data;
    public BinaryNode<E> left, right, parent;
}
```

线索二叉树二叉链表
```java
public class BinaryNode<E>
{
    public E data;
    public BinaryNode<E> left, right;
    public int leftTag, rightTag;
}
```

## 遍历
先序遍历
```java
// 访问根接点，遍历左子树，遍历右子树
public void preOrder(BinaryNode<E> node)
{
    // print node
    preOrder(node.left);
    preOrder(node.right);
}
```

中序遍历
```java
// 遍历左子树，访问根接点，遍历右子树
public void inOrder(BinaryNode<E> node)
{
    inOrder(node.left);
    // print node
    inOrder(node.right);
}
```

后序遍历
```java
// 遍历左子树，遍历右子树，访问根接点
public void postOrder(BinaryNode<E> node)
{
    postOrder(node.left);
    postOrder(node.right);
    // print node
}
```

层次遍历
```java
// 从根节点开始，逐层深入，从左至右依次访问完当前层的所有结点，再访问下一层。
public void levelOrder(BinaryNode<E> node)
{
    // print node
}
```
