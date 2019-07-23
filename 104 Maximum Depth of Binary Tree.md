# 104 Maximum Depth of Binary Tree

## 题目描述

给定一棵二叉树，求其最大深度。

## 怎么解的

递归

 ```java
 public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        } else return 1+ Math.max(maxDepth(root.left), maxDepth(root.right));
    }
 ```
