# 669. Trim a Binary Search Tree

## 题目

给定一个BST以及下界L，上界R。将BST中不在`[L, R]`范围内的节点删除，同时使整棵树仍然保持是BST（可能要改变根节点）。

>Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in `[L, R] (R >= L)`. You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.
>
>Example 1:
>
>>```java
>>Input:  
>>
>>   1
>>  / \
>> 0   2
>>
>>  L = 1
>>  R = 2
>>
>>Output:
>>   1
>>    \
>>     2
>>```
>
>Example 2:
>
>>```java
>>Input:  
>>    3
>>   / \
>>  0   4
>>   \
>>    2
>>   /
>>  1
>>
>>  L = 1
>>  R = 3
>>
>>Output:
>>      3
>>     /
>>   2
>>  /
>> 1
>>```

## 解法

递归的解法。如果`root.val > R`， 那么包括根节点和右子树肯定需要被剪掉，我们从`root.left`开始找起。类似的如果`root.val < L`， 则根节点和左子树都要被剪掉。

```java
public TreeNode trimBST(TreeNode root, int L, int R) {
        if (root == null) return null;
        if (root.val < L) return trimBST(root.right, L, R);
        if (root.val > R) return trimBST(root.left, L, R);
        root.left = trimBST(root.left, L, R);
        root.right = trimBST(root.right, L, R);
        return root;
    }
```

时间复杂度和空间复杂度O(N)
