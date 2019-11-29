# 1022. Sum of Root To Leaf Binary Numbers

## 题目

一个二叉树，节点元素不是0就是1。从根节点开始到叶子节点组成的01字符串表示一个二进制数（根节点元素为最高位）。求所有这样的二进制数对应的十进制之和。

>Given a binary tree, each node has value 0 or 1.  Each root-to-leaf path represents a binary number starting with the most significant bit.  For example, if the path is 0 -> 1 -> 1 -> 0 -> 1, then this could represent 01101 in binary, which is 13.
>
>For all leaves in the tree, consider the numbers represented by the path from the root to that leaf.
>
>Return the sum of these numbers.
>
>**Example 1:**
>
>>Input: [1,0,1,0,1,0,1]  
>>Output: 22  
>>Explanation: (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
>
>**Note:**
>
> - The number of nodes in the tree is between 1 and 1000.
> - node.val is 0 or 1.
> - The answer will not exceed 2^31 - 1.

## 解法

递归咯。拿全局变量存元素之和sum，当递归到叶子节点时把thisNum加进去。

时间复杂度O(N)，空间复杂度由函数的调用栈产生。

```java
 private int sum = 0;
    public int sumRootToLeaf(TreeNode root) {
        helper(root, 0);
        return sum;
    }

    private void helper(TreeNode node, int thisNum){
        if (node == null) return;
        thisNum = thisNum*2 + node.val;
        if (node.left == null && node.right == null) {sum+=thisNum; return;}
        helper(node.left, thisNum);
        helper(node.right, thisNum);
    }
```
