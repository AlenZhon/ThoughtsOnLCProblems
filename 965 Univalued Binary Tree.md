# 965. Univalued Binary Tree

## 题目

判断一个二叉树里的节点值是否是同一个值。二叉树节点个数在`[1,100]`范围内，节点的值在`[0,99]`范围内。

>A binary tree is univalued if every node in the tree has the same value.
>
Return true if and only if the given tree is univalued.
>
>**Example 1:**
>
>>Input: `[1,1,1,1,1,null,1]`
>>Output: true
>
>**Example 2:**
>
>>Input: `[2,2,2,5,2]`  
>>Output: false
>
>Note:
>
> - The number of nodes in the given tree will be in the range `[1, 100]`.
> - Each node's value will be an integer in the range `[0, 99]`.

## 解法

写就完事了。

### recursive

```java
public boolean isUnivalTree(TreeNode root) {
        if (root == null) return true;
        if (root.left!= null && root.val != root.left.val) return false;
        if (root.right != null && root.val != root.right.val) return false;
        return isUnivalTree(root.left) && isUnivalTree(root.right);
    }
```

### Iterative

```java
public boolean isUnivalTree(TreeNode root) {
        Queue<TreeNode> q = new LinkedList();
        q.add(root);
        int val = root.val;
        while (!q.isEmpty()){
            TreeNode curr = q.poll();
            if (curr != null && val != curr.val) return false;
            if (curr.left != null) q.add(curr.left);
            if (curr.right != null) q.add(curr.right);
        }
        return true;
    }
```
