# 872. Leaf-Similar Trees

## 题目

将一棵二叉树的叶子结点从左至右组成一个叶节点序列。现在给定两棵二叉树，判断它们的叶节点序列是否相同。

## 解法

对两棵树分别用DFS。时间复杂度 O(T1 + T2)，空间复杂度也为 O(T1 + T2)。其中T1, T2分别为两棵树的节点个数。

```java
public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        List<Integer> leaf1 = new ArrayList<>();
        List<Integer> leaf2 = new ArrayList<>();
        dfs(root1, leaf1);
        dfs(root2, leaf2);
        return leaf1.equals(leaf2);
    }
    private void dfs(TreeNode root, List<Integer> leaf){
        if (root != null) {
            if (root.left == null && root.right == null)
                leaf.add(root.val);
            dfs(root.left, leaf);
            dfs(root.right, leaf);
        }
    }
```

这里用了`leaf1.equals(leaf2)`比较两个list对象是否相同。
