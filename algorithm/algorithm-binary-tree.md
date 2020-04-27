# 算法-二叉树

## 遍历
先序遍历
```java
final void preOrder()
{
    if (this.root == null)
    {
        return;
    }
    logger.info("{}", root);
    preOrder(root.getLeft());
    preOrder(root.getRight());
}

private void preOrder(Node<E, V> node)
{
    if (node == null)
    {
        return;
    }
    logger.info("{}", node);
    preOrder(node.getLeft());
    preOrder(node.getRight());
}
```

中序遍历
```java
final void inOrder()
{
    if (this.root == null)
    {
        return;
    }
    inOrder(root.getLeft());
    logger.info("{}", root);
    inOrder(root.getRight());
}

private void inOrder(Node<E, V> node)
{
    if (node == null)
    {
        return;
    }
    inOrder(node.getLeft());
    logger.info("{}", node);
    inOrder(node.getRight());
}
```

后序遍历
```java
final void postOrder()
{
    if (this.root == null)
    {
        return;
    }
    postOrder(root.getLeft());
    postOrder(root.getRight());
    logger.info("{}", root);
}

private void postOrder(Node<E, V> node)
{
    if (node == null)
    {
        return;
    }
    postOrder(node.getLeft());
    postOrder(node.getRight());
    logger.info("{}", node);
}
```

层次遍历
```java
final void levelOrder()
{
    try
    {
        LinkedBlockingQueue<Node<E, V>> queue = new LinkedBlockingQueue<>();
        Node<E, V> node = this.root;
        while (node != null)
        {
            logger.info("{}", node);
            if (node.getLeft() != null)
            {
                queue.put(node.getLeft());
            }
            if (node.getRight() != null)
            {
                queue.put(node.getRight());
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

Node.java
```java
public interface Node<E, V>
{
    V getValue();

    Node<E, V> getLeft();

    Node<E, V> getRight();

    Node<E, V> getParent();

    void setLeft(Node<E, V> node);

    void setRight(Node<E, V> node);

    void setParent(Node<E, V> node);
}
```

AbstractTree.java
```java
public abstract class AbstractTree<E, V> implements Tree<Node<E, V>>
{
    final Logger logger = LoggerFactory.getLogger(this.getClass());
    Node<E, V> root;
    List<Node<E, V>> nodes;

    AbstractTree(Node<E, V> root)
    {
        this.root = root;
        this.nodes = Lists.newArrayList(root);
    }

    @Override
    public boolean isEmpty()
    {
        return this.root == null;
    }

    @Override
    public void clear()
    {
        this.nodes.clear();
    }

    @Override
    public Node<E, V> getRoot()
    {
        return this.root;
    }
}
```
