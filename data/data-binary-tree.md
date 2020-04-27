# 二叉树

|种类|顺序存储结构|链式存储结构|备注|
|---|---|---|---|
|完全二叉树|√||
|满二叉树|√||
|二叉搜索树||√||
|线索二叉树||√|按某种遍历次序进行线索化的二叉树|
|哈夫曼树||√|哈夫曼编码是一种无损压缩<br>获得哈夫曼编码的过程也就是建立哈夫曼树的过程|
|红黑树||√||
|B树||√||

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
