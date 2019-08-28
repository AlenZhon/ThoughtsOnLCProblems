# 226. Invert Binary Tree

## 题目

给定一二叉树，返回其左右翻转后的二叉树。

>Invert a binary tree.
>
>**Example:**
>
>Input:
>
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4  
>>&nbsp;&nbsp;&nbsp;&nbsp;/ \  
>>&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;7  
>>&nbsp;&nbsp;/ \ / \  
>>&nbsp;1  3 6   9  
>
>Output:
>
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4  
>>&nbsp;&nbsp;&nbsp;&nbsp;/   \  
>>&nbsp;&nbsp;&nbsp;7&nbsp;&nbsp;2  
>>&nbsp;&nbsp;/ \   / \  
>>&nbsp;9   6 3   1  
>
>Trivia:
>This problem was inspired by this original tweet by Max Howell:
>
>>Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

## 解法

最爽的肯定是递归解法了。时间复杂度O(n)，空间复杂度O(height of binary tree)近似等于O(n)。

```java
public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        else if (root.left == null && root.right == null) return root;
        else if (root.left != null || root.right != null) {
            TreeNode p1 = invertTree(root.right);
            TreeNode p2 = invertTree(root.left);
            root.left =p1;
            root.right = p2;
        }
        return root;
    }
```

其实不需要分三种情况，只需把`root == null`单摘出来就可以了，其他情况都是要交换的。还是思路不清晰。

```java
 public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode p1 = invertTree(root.right);
        TreeNode p2 = invertTree(root.left);
        root.left =p1;
        root.right = p2;
        return root;
    }
```

如果用Iterative的方法，可维护一个队列，对每个节点交换左节点和右节点，并加入到队列中。时间和空间复杂度都为O(n)

```java
public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            TreeNode temp = curr.left;
            curr.left = curr.right;
            curr.right = temp;
            if (curr.left != null) q.add(curr.left);
            if (curr.right != null) q.add(curr.right);
        }
        return root;
    }
```

## Notes

二叉树的相关题目还有*101 Symmetric Tree*， *100 Same Tree*等。
