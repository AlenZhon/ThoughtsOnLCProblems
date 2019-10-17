# 563. Binary Tree Tilt

## 题目

给定一二叉树，返回整个二叉树的tilt。  
对于一个节点，计算其左子树所有节点值之和与右子树所有节点值之和，计算两个和的绝对差值，即为这个节点的tilt。叶节点的tilt为0。
>Given a binary tree, return the tilt of the whole tree.
>
>The tilt of a tree node is defined as the absolute difference between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.
>
>The tilt of the whole tree is defined as the sum of all nodes' tilt.
>
>**Example:**
>
>>Input:  
>>
>>```java
>>       1
>>     /   \
>>    2     3
>>```
>>
>>Output: 1  
>>Explanation:  
>>Tilt of node 2 : 0  
>>Tilt of node 3 : 0  
>>Tilt of node 1 : |2-3| = 1  
>>Tilt of binary tree : 0 + 0 + 1 = 1  
>
>**Note:**
>
> - The sum of node values in any subtree won't exceed the range of 32-bit integer.
> - All the tilt values won't exceed the range of 32-bit integer.

## 解法

由于要记录下每个节点的tilt，并且递归的时候需要计算节点值之和，所以使用了一个全局变量做累加。

```java
 int sum =0;
    public int findTilt(TreeNode root) {
        helper(root);
        return sum;
    }
    private int helper(TreeNode node){
        if (node == null) return 0;
        int left = helper(node.left);
        int right = helper(node.right);
        sum += Math.abs(left - right);
        return left + right + node.val;
    }
```

如果不用全局变量，想到的是用ArrayList做传入参数，最后累加ArrayList中存储的每个节点的tilt。

```java
public int findTilt(TreeNode root) {
        ArrayList<Integer> tilt = new ArrayList<>();
        helper(root, tilt);
        int sum = 0;
        for (Integer i : tilt)
            sum+= i;
        return sum;
    }
    private int helper(TreeNode node, List<Integer> list){
        if (node == null) return 0;
        int left = helper(node.left, list);
        int right = helper(node.right, list);
        int tilt = Math.abs(left - right);
        list.add(tilt);
        return left + right + node.val;
    }
```
