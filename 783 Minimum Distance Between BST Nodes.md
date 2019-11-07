# 783. Minimum Distance Between BST Nodes

## 题目

给定一个二叉搜索树，元素均为整数且各不相同。求出树中任意两节点元素的差值最小值。

>Given a Binary Search Tree (BST) with the root node root, return the minimum difference between the values of any two different nodes in the tree.
>
>Example :
>>
>>```java
>>Input: root = [4,2,6,1,3,null,null]
>>Output: 1
>>Explanation:
>>Note that root is a TreeNode object, not an array.
>>
>>The given tree [4,2,6,1,3,null,null] is >>represented by the following diagram:
>>
>>          4
>>        /   \
>>      2      6
>>     / \
>>    1   3  
>>
>>while the minimum difference in this tree is 1, it occurs between node 1 and node 2, also between node 3 and node 2.
>>```
>
>Note:
>
> - The size of the BST will be between 2 and 100.
> - The BST is always valid, each node's value is an integer, and each node's value is different.

## 解法

和 *530 Minmum Absolute Difference in BST* 非常相似。中序遍历则BST的元素按顺序遍历到。设两个私有变量`prev, min`。保存上一个元素值为`prev`，并计算`min = Math.min(min, root.val - prev)`即可。

```java
    private int min = Integer.MAX_VALUE, prev = Integer.MIN_VALUE;
    public int minDiffInBST(TreeNode root) {
        inOrder(root);
        return min;
    }
    private void inOrder(TreeNode root) {
        if (root == null) return;
        inOrder(root.left);
        if (prev > Integer.MIN_VALUE) min = Math.min(min, root.val - prev);
        prev = root.val;
        inOrder(root.right);
    }
```
