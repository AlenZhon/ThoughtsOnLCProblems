# 700. Search in a Binary Search Tree

## 题目

给定一个二叉搜索树BST和一个元素值，返回以该元素值为根节点的子树。如果BST中不存在该元素，返回null。

>Given the root node of a binary search tree (BST) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.
>
>For example,
>
>Given the tree:
>
>>```java
>>      4
>>     / \
>>    2   7
>>   / \
>>  1   3
>>
>>And the value to search: 2
>>You should return this subtree:
>>
>>      2
>>     / \
>>    1   3
>>```
>
>In the example above, if we want to search the value 5, since there is no node with value 5, we should return `NULL`.
>
>Note that an empty tree is represented by `NULL`, therefore you would see the expected output (serialized tree format) as [], not null.

## 解法

水题。用BST的性质就完事了。

```java
public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) return null;
        if (root.val > val)
            return searchBST(root.left, val);
        else if (root.val < val)
            return searchBST(root.right, val);
        return root;
    }
```

如果BST中允许出现相同元素（比如左子树的节点都不大于根节点，右子树的节点都大于根节点），则按照程序走，返回的是相同元素中最靠近根节点的子树？
