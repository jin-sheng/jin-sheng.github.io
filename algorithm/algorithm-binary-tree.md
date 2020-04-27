# 算法-二叉树

## 遍历
先序遍历
```java
public void preOrder()
{
    if (this.root == null)
    {
        return;
    }
    logger.info("{}", root);
    preOrder(root.left);
    preOrder(root.right);
}

private void preOrder(BinaryNode node)
{
    if (node == null)
    {
        return;
    }
    logger.info("{}", node);
    preOrder(node.left);
    preOrder(node.right);
}
```

中序遍历
```java
public void inOrder()
{
    if (this.root == null)
    {
        return;
    }
    inOrder(root.left);
    logger.info("{}", root);
    inOrder(root.right);
}

private void inOrder(BinaryNode node)
{
    if (node == null)
    {
        return;
    }
    inOrder(node.left);
    logger.info("{}", node);
    inOrder(node.right);
}
```

后序遍历
```java
public void postOrder()
{
    if (this.root == null)
    {
        return;
    }
    postOrder(root.left);
    postOrder(root.right);
    logger.info("{}", root);
}

private void postOrder(BinaryNode node)
{
    if (node == null)
    {
        return;
    }
    postOrder(node.left);
    postOrder(node.right);
    logger.info("{}", node);
}
```

层次遍历
```java
public void levelOrder()
{
    try
    {
        LinkedBlockingQueue<BinaryNode<E>> queue = new LinkedBlockingQueue<>();
        BinaryNode<E> node = this.root;
        while (node != null)
        {
            logger.info("{}", node);
            if (node.left != null)
            {
                queue.put(node.left);
            }
            if (node.right != null)
            {
                queue.put(node.right);
            }
            node = queue.poll();
        }
    }
    catch (Exception e)
    {
        logger.error(e.getMessage(), e);
    }
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
