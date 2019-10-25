# 671. Second Minimum Node In a Binary Tree

## 题目

有一种特殊的二叉树，它的构成是这样的： 对于一个非叶子结点，它有0或2个子节点。如果有两个子节点，则节点的值等于子节点的最小值。现在给定一棵这样的树，求树中第二小的节点值。

>Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly `two` or `zero` sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property `root.val = min(root.left.val, root.right.val)` always holds.
>
>Given such a binary tree, you need to output the **second minimum** value in the set made of all the nodes' value in the whole tree.
>
>If no such second minimum value exists, output `-1` instead.
>
>Example 1:
>
>>```java
>>Input:
>>   2
>>  / \
>> 2   5
>>    / \
>>   5   7
>>
>>Output: 5
>>Explanation: The smallest value is 2, the second smallest value is 5.
>>```
>
>Example 2:
>
>>```java
>>Input:
>>   2
>>  / \
>> 2   2
>>
>>Output: -1
>>Explanation: The smallest value is 2, but there isn' t any second smallest value.

## 解法

一开始没看清题目以为是BST，总是右边节点值比左边的大。因为没有这条性质，所以第二小的节点值左右子树都可能出现。

粗暴的方法就是把二叉树遍历后排序，找到第二小的元素。时间复杂度O(nlogn)空间复杂度O(n)

稍作修改，可以在遍历时用set存储节点值，这样就不需要之后的排序。时间复杂度降到遍历的O(n)。

```java
private void dfs(TreeNode root, Set<Integer> set) {
        if (root == null) return;
        set.add(root.val);
        dfs(root.left, set);
        dfs(root.right, set);
    }
    public int findSecondMinimumValue(TreeNode root) {
        Set<Integer> set = new HashSet<>();
        dfs(root,set);
        int min1 = root.val;
        long ans = Long.MAX_VALUE;
        for (int i : set)
            if (min1 < i && i <ans) ans =i;
        return ans < Long.MAX_VALUE ? (int) ans : -1;
    }
```

实际上，如果子节点的值比当前节点的值大，那么第二小的值不会在该子树里面。

```java
    int min;
    long ans = Long.MAX_VALUE;

    public int findSecondMinimumValue(TreeNode root) {
        min = root.val;
        dfs(root);
        return ans < Long.MAX_VALUE ? (int) ans : -1;
    }

    public void dfs(TreeNode root){
        if(root != null){
            if(min < root.val && root.val < ans){
                ans = root.val;
            }
            else if(min == root.val){
                dfs(root.left);
                dfs(root.right);
            }
        }
    }
```
