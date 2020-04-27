# 二叉树

|种类|顺序存储结构|链式存储结构|备注|
|---|---|---|---|
|完全二叉树|√||
|满二叉树|√||
|二叉搜索树||√||
|线索二叉树||√||
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

## 类
Tree.java
```java
public interface Tree<T>
{
    T getRoot();

    T search(T node);

    void insert(T node);

    void delete(T node);

    boolean isEmpty();

    void clear();
}
```

BinaryNode.java
```java
public class BinaryNode<T>
{
    public T value;
    public BinaryNode<T> left, right, parent;

    public BinaryNode(T value)
    {
        this.value = value;
    }

    public BinaryNode(T value, BinaryNode<T> left, BinaryNode<T> right)
    {
        this.value = value;
        this.left = left;
        this.right = right;
    }
}
```

BinaryTree.java
```java
public class BinaryTree<E> implements Tree<BinaryNode<E>>
{
    public BinaryNode<E> root;
    
    public BinaryTree(BinaryNode<E> root)
    {
        this.root = root;
    }
    
    public boolean isEmpty()
    {
        return this.root == null;
    }
    
    public BinaryNode<E> getRoot()
    {
        return this.root;
    }
}
```
