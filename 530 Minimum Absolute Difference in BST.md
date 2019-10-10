# 530. Minimum Absolute Difference in BST

## 题目

一棵二叉搜索树，找出两两节点之间最小的距离。

>Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.
>
>**Example:**
>
>Input:
>
>&nbsp;&nbsp;1  
>&nbsp;&nbsp;&nbsp;\  
>&nbsp;&nbsp;&nbsp;&nbsp;3  
>&nbsp;&nbsp;&nbsp;/  
>&nbsp;2
>
>Output:  
>1
>
>Explanation:  
>The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
>
>Note: There are at least two nodes in this BST.

## 解法

笨办法。维护一个`ArrayList`，对BST做中序遍历，则遍历得到的数列肯定按照升序排列。遍历数列取差值最小。

```java
public int getMinimumDifference(TreeNode root) {
        inOrder(root);
        Integer[] array = node.toArray(new Integer[node.size()]);
        int minimum = Integer.MAX_VALUE;
        for (int i = 1; i< array.length; i++)
            minimum = Math.min(minimum, array[i] - array[i - 1]);
        return minimum;
    }

    private List<Integer> node = new ArrayList<Integer>();
    private void inOrder(TreeNode root) {
        if (root == null) return;
        inOrder(root.left);
        node.add(root.val);
        inOrder(root.right);
    }
```

时间复杂度由递归和遍历两部分组成。空间复杂度O(n)。

实际上可以用`TreeNode prev`存储前一个节点。根据BST的性质，`prev`存储的顺序正是中序遍历的节点顺序。这样便可在递归过程中完成计算。

```java
 public int getMinimumDifference(TreeNode root) {
        inOrder(root);
        return min;
    }

    private int min = Integer.MAX_VALUE;
    private TreeNode prev;
    private void inOrder(TreeNode root) {
        if (root == null) return;
        inOrder(root.left);
        if (prev != null) min = Math.min(min, Math.abs(root.val - prev.val));
        prev = root;
        inOrder(root.right);
    }
```
