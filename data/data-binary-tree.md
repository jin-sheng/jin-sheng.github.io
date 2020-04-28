# 二叉树

## 概览

|种类|顺序存储|链式存储|应用|备注|
|---|---|---|---|---|
|完全二叉树|√||||
|满二叉树|√||||
|线索二叉树||√||按某种遍历次序进行线索化的二叉树<br>直接找到某结点在某种遍历次序下的前驱或后继结点|
|二叉搜索树<br>二叉查找树<br>二叉排序树||√|路由器搜索引擎|对任何结点 x<br>其左子树中的所有关键字都比 x 小<br>其右子树中的所有关键字都比 x 大|
|平衡二叉树||√|Windows NT 内核|高度平衡的二叉搜索树|
|红黑树||√|HashMap<br>TreeMap<br>IO 多路复用 epoll<br>Linux 进程调度|保证在最坏情况下基本动态集合操作的时间复杂度为 O(lgn)|
|哈夫曼树||√|数据压缩|哈夫曼编码是一种无损压缩<br>获得哈夫曼编码的过程也就是建立哈夫曼树的过程|

## 动态集合操作

|操作|说明|二叉树种类|时间复杂度|
|---|---|---|---|
|PREORDER-TREE-WALK|先序遍历|||
|||完全二叉树||
|||二叉搜索树||
|||平衡二叉树||
|||红黑树||
|INORDER-TREE-WALK|中序遍历|||
|||完全二叉树||
|||二叉搜索树||
|||平衡二叉树||
|||红黑树||
|POSTORDER-TREE-WALK|后序遍历|||
|||完全二叉树||
|||二叉搜索树||
|||平衡二叉树||
|||红黑树||
|LEVELORDER-TREE-WALK|层次遍历|||
|||完全二叉树||
|||二叉搜索树||
|||平衡二叉树||
|||红黑树||
|SEARCH|查找指定结点|||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|MINIMUM|查找最小关键字结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|MAXIMUM|查找最大关键字结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|SUCCESSOR|查找后继结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|PREDECESSOR|查找前驱结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|INSERT|插入指定结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||
|DELETE|删除指定结点||
|||完全二叉树|<=O(lgn)|
|||二叉搜索树|<=O(h)|
|||平衡二叉树||
|||红黑树||

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

# 参考
[一文读懂平衡二叉树｜技术头条](https://baijiahao.baidu.com/s?id=1646617486319372351&wfr=spider&for=pc)  
