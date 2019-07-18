# 101 Symmetric Tree

## 题目描述

给定一棵二叉树，判断该树是否对称

>For example, this binary tree [1,2,2,3,4,4,3] is symmetric:  
>
>But the following [1,2,2,null,3,null,3] is not:

## 怎么解的

肯定有两种方法： Recursion & Iteration.

1. 一棵树镜像对称等价于它的左子树和右子树是对称的。
2. 如何判断左右子树对称（设两子树根节点为A B）？  
2.1 A B均为空，则肯定是对称的  
2.2 A B元素不相等，则肯定不对称  
2.3 A B相等，则比较（A的左子树和B的右子树是否对称）&& （A的右子树和B的左子树是否对称）

```java
public boolean isSymmetric(TreeNode root) {
        if (root == null) { //leetcode测试样例里好像没有这种情况
            return true;
        } else return checkSymmetric(root.left, root.right);
    }
    public boolean checkSymmetric(TreeNode lnode, TreeNode rnode) {
        if (lnode == null && rnode == null) return true;
        if (lnode == null || rnode == null || lnode.val != rnode.val) return false;
        return checkSymmetric(lnode.left, rnode.right) && checkSymmetric(lnode.right, rnode.left);
    }
```

递归的方法时间复杂度为O(n)

迭代的方法我使用了Stack实现

```java
 public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        Stack<TreeNode> s = new Stack<TreeNode>();
        s.push(root.left);
        s.push(root.right);
        while (!s.empty()) {
            TreeNode p = s.pop();
            TreeNode q = s.pop();
            if (p == null && q == null) continue;
            if (p == null || q == null) return false;
            if (p.val != q.val) return false;
            s.push(p.left);
            s.push(q.right);
            s.push(p.right);
            s.push(q.left);
        }
        return true;
    }
```
