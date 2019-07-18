# 100 Same Tree

## 题目描述

给定两棵二叉树，检查这两棵二叉树是否相同。相同的定义为：具有相同的结构，对应节点的数值相同。

## 怎么解的

递归。排除false的情况，按照p和q的左节点和右节点递归。

```java
public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null || p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
```

设二叉树中节点数量为n,则时间复杂度为O(n)。
