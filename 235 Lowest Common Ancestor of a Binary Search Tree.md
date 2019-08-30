# 235. Lowest Common Ancestor of a Binary Search Tree

## 题目

给定一个二叉搜索树和其中的两个节点，找出这两个节点的LCA。允许一个节点同时是自己的前驱。

>Given a binary search tree (BST), find the `lowest common ancestor` (LCA) of two given nodes in the BST.
>
>According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (**where we allow a node to be a descendant of itself**).”
>
>Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]
>
>**Example 1:**
>
>>Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8  
>>Output: 6  
>>Explanation: The LCA of nodes 2 and 8 is 6.
>
>**Example 2:**
>
>>Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4  
>>Output: 2  
>>Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
>
>Note:
>
> - All of the nodes' values will be unique.
> - p and q are different and both values will exist in the BST.

## 解法

BST，也就是二分搜索树。它满足以下几个条件：

1. 若节点的左子树非空，则左子树上的所有值都小于节点的值
2. 若节点的右子树非空，则右子树上的所有值都大于节点的值。
3. 节点的左子树和右子树也是二分搜索树。

### recursive

根据这个性质，很容易找到递归方法的思路：判断当前节点的值与`p.val, q.val`的大小，分情况搜索左子树或右子树。时间复杂度O(N)，空间复杂度O(N)，N为BST中节点总个数。

```java
 public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val == p.val ||root.val == q.val) return root;
        if (root.val > p.val && root.val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        else if (root.val < p.val && root.val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        else return root;
    }
```

### Iterative

类似可写出迭代的方法。

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val == p.val ||root.val == q.val) return root;
        TreeNode curr = root;
        while (curr != null) {
            if (curr.val > p.val &&curr.val > q.val) curr =curr.left;
            else if (curr.val < p.val && curr.val < q.val) curr = curr.right;
            else return curr;
        }
        return null;
    }
```

时间复杂度O(N)，空间复杂度O(1)。  
