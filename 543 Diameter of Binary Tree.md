# 543. Diameter of Binary Tree

## 题目

给定一棵二叉树，求树中任意两个节点相距的最远距离。此最远距离可能经过（也可能不经过）根节点。

>Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. This path may or may not pass through the root.
>
>**Example:**
>Given a binary tree
>
>```java
>          1
>         / \
>        2   3
>       / \
>      4   5
>```
>
>Return **3**, which is the length of the path [4,2,1,3] or [5,2,1,3].
>
>**Note:** The length of path between two nodes is represented by the number of edges between them.

## 解法

这个`may or may not`就很灵性。

分析题目，发现题目要求的是相距最远的两个叶节点。  
如果最长路径经过根节点，则两个叶节点分别属于根节点的左右子树，它们相距根节点必最远。  
如果不经过根节点，则两个叶节点相距它们共同的子树根节点最远。

在DFS中需要记录两个变量，一个是当前子树中能构成的最长路径，另一个是当前子树的最大深度。所以递归的时候返回的是最大深度，用全局变量`maxDistance`记录当前的最长路径。

时间复杂度和空间复杂度应都是O(N)，和节点个数有关。

```java
    private int maxDistance = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) return maxDistance;
        getDistance(root);
        return maxDistance;
    }
    private int getDistance(TreeNode root) {
        if (root == null) return -1;
        int maxLeft = getDistance(root.left);
        int maxRight = getDistance(root.right);
        maxDistance = Math.max(maxDistance, maxLeft + maxRight +2);
        return Math.max(maxLeft, maxRight) + 1;
    }
```
