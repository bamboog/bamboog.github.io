---
layout: post
title:  红黑树
date: 2016-01-01
tags: java
---

## 简介
- HashMap，如果hash冲突会使用链表，如果冲突链表size大于8，就会使用红黑树代替链表（1.8后），为什么会这样做，这样做有什么好处？
- TreeMap 使用红黑树实现，处于什么考虑？
## 来源
红黑树是一种近似平衡的二叉查找树，它能够确保任何一个节点的左右子树的高度差不会超过二者中较低那个的一陪。
具体来说，红黑树是满足如下条件的二叉查找树（binary search tree）：
- 每个节点要么是红色，要么是黑色。
- 根节点必须是黑色
- 红色节点不能连续（也即是，红色节点的孩子和父亲都不能是红色）。
- 对于每个节点，从该点至null（树尾端）的任何路径，都含有相同个数的黑色节点。

看到这样一个定义，我反正已经崩溃了；还好可以追本溯源：
##### 溯源
- 二叉树-->搜索二叉树-->平衡搜索二叉树--> 红黑树
- Binary Search Tree，简称BST --> 平衡二叉查找树(Balanced BST)
- Balanced BST -->  2-3 Search Tree
- 2-3 Search Tree --> Red-Black Tree

######## 演化过程
- BST
  - 图示
  ![](https://bamboog.github.io/images/java/bst.jpg)
  - 问题很明显，有可能出现右侧树，查询效率就是O(n)了

- BBST
  - 考虑使用平衡，解决了BST问题
  - 维持树的平衡太费劲--具体分析？

- 2-3 ST
  - 解决了BBST问题
  - 损失了完全平衡
  - 实现复杂（主要是多种数据节点，自己是否可以实现？）

- RBT
  - 2-3 ST -- 可实现版本

- 对比图
![](https://bamboog.github.io/images/java/23-rbt.jpg)









## 使用
