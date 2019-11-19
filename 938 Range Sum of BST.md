# 938. Range Sum of BST

## 题目

给定一个BST，和元素的上下界`[L, R]`（保证上界不小于下界），求BST中在[L, R]的元素之和。BST中元素保证是各不相同的。

>Given the root node of a binary search tree, return the sum of values of all nodes with value between L and R (inclusive).
>
>The binary search tree is guaranteed to have unique values.
>
>**Example 1:**
>
>>Input: root = [10,5,15,3,7,null,18], L = 7, R = 15  
>>Output: 32
>
>**Example 2:**
>
>>Input: root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10  
>>Output: 23
>
>**Note:**
>
> - The number of nodes in the tree is at most 10000.
> - The final answer is guaranteed to be less than 2^31.

## 解法

水题。时间复杂度O(N)，空间复杂度O(H)，`N H` 分别为BST的节点个数和高度。

### recursive

一个全局变量作为加和。

```java
    private int sum = 0;
    public int rangeSumBST(TreeNode root, int L, int R) {
        dfs(root, L, R);
        return sum;
    }

    private void dfs(TreeNode root, int L, int R) {
        if (root == null) return;
        if (root.val >= L && root.val <= R) sum+=root.val;
        if (root.val > L) dfs(root.left, L, R);
        if (root.val < R) dfs(root.right, L, R);
    }
```

不用全局变量也可以。用返回值记录元素之和。

```java
public int rangeSumBST(TreeNode root, int L, int R) {
        if (root == null) return 0;
        int ret = 0;
        if (root.val >= L && root.val <= R) ret+= root.val;
        if (root.val < R) ret += rangeSumBST(root.right, L, R);
        if (root.val > L) ret += rangeSumBST(root.left, L, R);
        return ret;
    }
```

### Iterative

```java
public int rangeSumBST(TreeNode root, int L, int R) {
        int ret = 0;
        Queue<TreeNode> q = new LinkedList();
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node != null) {
                if (node.val >= L && node.val <= R) ret+= node.val;
                if (node.val < R) q.offer(node.right);
                if (node.val > L) q.offer(node.left);
            }
        }
        return ret;
    }
```
