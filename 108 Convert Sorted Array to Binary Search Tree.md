# 108. Convert Sorted Array to Binary Search Tree

## 题目

给定一个升序数列，用这个数列生成一个二叉搜索树。要求搜索树是平衡的，即所有叶子节点的深度的最大差值不超过1。

>Given an array where elements are sorted in ascending order, convert it to a height balanced BST.
>
>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
>
>**Example:**
>
>Given the sorted array: `[-10,-3,0,5,9]`,
>
>One possible answer is: `[0,-3,9,-10,null,5]`, which represents the following height balanced BST:
>>
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0  
>>&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp; \  
>>&nbsp;&nbsp;-3&nbsp;&nbsp;&nbsp;9  
>>&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;/  
>>-10&nbsp;&nbsp;5

## 解法

题目暗示了对于任一数列，生成BST的可行解不止一种。  
递归求的解。一开始生成出错有好几个元素没有出现在树里，debug了好久发现判断返回null的条件是`(start > end)`不能取等。

```java
public TreeNode sortedArrayToBST(int[] nums) {
        int n = nums.length;
        return arrayToBST(0, n - 1, nums);
    }

    private TreeNode arrayToBST(int start, int end, int[] nums) {
        if (start > end) return null;
        int mid = start + (end - start) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = arrayToBST(start, mid - 1, nums);
        node.right = arrayToBST(mid + 1, end, nums);
        return node;
    }
```
