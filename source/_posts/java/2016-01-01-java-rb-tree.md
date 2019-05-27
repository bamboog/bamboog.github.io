---
layout: post
title:  红黑树
date: 2016-01-01
tags: java
---

### 简介
- HashMap，如果hash冲突会使用链表，如果冲突链表size大于8，就会使用红黑树代替链表（1.8后），为什么会这样做，这样做有什么好处？
- TreeMap 使用红黑树实现，处于什么考虑？
### 定义
红黑树是一种近似平衡的二叉查找树，它能够确保任何一个节点的左右子树的高度差不会超过二者中较低那个的一陪。
具体来说，红黑树是满足如下条件的二叉查找树（binary search tree）：
- 每个节点要么是红色，要么是黑色。
- 根节点必须是黑色
- 红色节点不能连续（也即是，红色节点的孩子和父亲都不能是红色）。
- 对于每个节点，从该点至null（树尾端）的任何路径，都含有相同个数的黑色节点。

<!-- more -->

看到这样一个定义，我反正已经崩溃了；还好可以追本溯源：
##### 溯源
- 二叉树 --> 二叉搜索树 --> 平衡二叉搜索树 --> 2-3搜索树 --> 红黑树
- Binary Search Tree，简称BST --> 平衡二叉查找树(Balanced BST)
- Balanced BST -->  2-3 Search Tree
- 2-3 Search Tree --> Red-Black Tree

##### 演化过程
- BST--二叉搜索树
  - 图示
  ![](https://bamboog.github.io/images/java/bst.jpg)
  - 问题很明显，有可能出现右侧树，查询效率就是O(n)了

- BBST--平衡二叉搜索树
  - 考虑使用平衡，解决了BST问题
  - 维持树的平衡太费劲--具体分析？

- 2-3 ST（2-3搜索树）
  - 解决了BBST问题
  - 损失了完全平衡
  - 实现复杂（主要是多种数据节点，自己是否可以实现？）

- RBT--红黑树
  - 2-3 ST -- 可实现版本

- 对比图
![](https://bamboog.github.io/images/java/23-rbt.jpg)


##### 更贴切的定义
红黑树是一种具有红色和黑色链接的平衡查找树，同时满足：
- 红色节点向左倾斜
- 一个节点不可能有两个红色链接
- 整个树完全黑色平衡，即从根节点到所以叶子结点的路径上，黑色链接的个数都相同。

##### 定义抽象规则化
- 节点的右子节点为红色，且左子节点位黑色，则左旋
- 节点的左子节点为红色，并且左子节点的左子节点也为红色，则右旋（怎么判断子子问题，怎么判断父子节点颜色？--全部轮询么？）
- 节点的左右子节点均为红色，则改变颜色，提升中间结点。

##### 伪代码
```java
add(node,key,value){
  //add_data
  if(node == null) new node(red);
  if(key < node.key) add(node.left,key,value);
  if(key > node.key) add(node.right,key,value);
  else node.value = value;

  // Balanced
  if((node.right.color == red) && (node.left.color == black)) rotateLeft(node);

  if((node.left.color == red) && (node.left.left.color == red)) rotateRight(node);

  if((node.right.color == red) && (node.left.color == red)) changeColor(node);
  }
```
#### 其它代码

``` java
//左旋
rotateLeft(node){
  right = node.right;
  node.right = right.left;
  right.left = node;
  left.color = node.color;
  node.color = red;
  return left;
}

//右旋
rotateRight(node){
    left = node.Left;
    node.left = left.right;
    left.right = node;
    left.color = node.color;
    node.color = red;
    return left;
}

//改色
对子节点的连线设置为黑色，自己的颜色设置为红色
changeColor(node){

}
```

## Java使用

- HashMap--ConcurrentHashMap
- TreeMap
##### 备注
我现在的理解是put写的相对复杂，原因暂时没有深究；
旋转逻辑还好，代码类下：
```java
/** From CLR */
   private void rotateLeft(Entry<K,V> p) {
       if (p != null) {
           Entry<K,V> r = p.right;
           p.right = r.left;
           if (r.left != null)
               r.left.parent = p;
           r.parent = p.parent;
           if (p.parent == null)
               root = r;
           else if (p.parent.left == p)
               p.parent.left = r;
           else
               p.parent.right = r;
           r.left = p;
           p.parent = r;
       }
   }
```


#### 下一步
B+树
