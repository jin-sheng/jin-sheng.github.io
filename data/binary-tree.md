# 二叉树

|种类|存储结构|备注|
|---|---|---|
|完全二叉树|顺序存储结构||
|满二叉树|顺序存储结构||

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

## 二叉树类
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

    @Override
    public String toString()
    {
        return super.toString() + ", value = " + this.value;
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
