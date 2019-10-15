# 538. Convert BST to Greater Tree

## 题目

给定一个二叉搜索树BST，将其转换为greaterTree，其中每个节点的值变成当前节点的值加上BST中所有大于它的值之和。

>Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.
>
>Example:
>
>Input: The root of a Binary Search Tree like this:
>
>>```java
>>              5
>>            /   \
>>           2     13
>>```
>
>Output: The root of a Greater Tree like this:
>
>>```java
>>             18
>>            /   \
>>          20     13
>>```

## 解法

BST的任意一个节点，其左子树中节点的值都不大于它，其右子树中节点的值都不小于它。根据这个性质，如果对BST进行反中序遍历（右子树->节点->左子树）则只需维护一个sum变量即可。

时间复杂度和空间复杂度均为O(N)。

```java
private int add = 0;
    public TreeNode convertBST(TreeNode root) {
        greaterTree(root);
        return root;
    }
    private void greaterTree(TreeNode node) {
        if (node == null) return;
        greaterTree(node.right);
        add += node.val;
        node.val = add;
        greaterTree(node.left);
    }
```

Solution里还有一种神奇的[Reverse Morris In-order Traversal](https://leetcode.com/problems/convert-bst-to-greater-tree/solution/)。可以将空间复杂度降到O(1)。
