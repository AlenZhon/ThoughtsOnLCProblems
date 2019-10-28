# 687 Longest Univalue Path

## 题目

给定一个二叉树，找出路径上所有节点值都相同的最大路径长度。路径可能不经过根节点。

>Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.
>
>The length of path between two nodes is represented by the number of edges between them.
>
>Example 1:
>>
>>```java
>>Input:
>>
>>              5
>>             / \
>>            4   5
>>           / \   \
>>          1   1   5
>>
>>Output: 2
>>```
>
>Example 2:
>>
>>```java
>>Input:
>>
>>              1
>>             / \
>>            4   5
>>           / \   \
>>          4   4   5
>>
>>Output: 2
>>```
>
>**Note:** The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.

## 解法

考虑采用深度遍历的递归解法，时间复杂度O(n)。对于每个节点，判断其左子树和右子树的最长路径。如果左节点和右节点和此节点值相等，则路径长度分别加1。更新保存当前最长路径长度的全局变量max。递归返回的是此节点向左或向右的最长路径。

```java
private int max = 0;
    public int longestUnivaluePath(TreeNode root) {
        dfs(root);
        return max;
    }

    private int dfs(TreeNode root) {
        if (root == null) return 0;
        int left = dfs(root.left);
        int right = dfs(root.right);
        left = (root.left != null && root.val == root.left.val) ? left + 1 : 0;
        right =(root.right != null && root.val == root.right.val) ? right + 1 : 0;
        max = Math.max(max, left + right);
        return Math.max(left, right);
    }
```
