# Binary Tree 二叉树

## 定义

* at most 2 children per node
* exactly 1 root
* exactly 1 path between root and  any node

## 特殊

* empty tree是二叉树
* 只有一个节点是二叉树
* 有一个root和一个子节点是二叉树

## 术语

* root 没有父节点的节点
* leaf  没有子节点的节点

##  深度优先搜索

* 用stack来存储数据（先进后出的结构）
* 往stack放数据时，先放右孩子，再放左孩子
* 实际应该是左边优先
* stack不为空，则继续进行读取
* stack默认以root开始
* 可以用递归进行实现

## 广度优先搜素

* queue来存储数据
* 先放左孩子，后放右孩子
* 无法用递归进行实现