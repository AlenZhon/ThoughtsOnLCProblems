# 404. Sum of Left Leaves

## 题目

给定一棵二叉树，求其左叶子节点值的和。

>Find the sum of all left leaves in a given binary tree.
>
>Example:
>
>>&nbsp;&nbsp;&nbsp;3  
>>&nbsp;&nbsp;/&nbsp;\  
>>9  20  
>>&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;\  
>>&nbsp;15&nbsp;&nbsp;7
>
>There are two left leaves in the binary tree, with values **9** and **15** respectively. Return **24**.

## 解法

### recursive

- 1 当前节点为空则 `return 0;`
- 2 判断当前节点是否有左节点。  
  - 2.1 若有则判断是不是叶子节点  
    是叶子节点就加和，不是就将此左节点作为当前节点递归
- 3 当前节点右节点递归。

```java
public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        int ans = 0;
        if (root.left != null) {
            if (root.left.left == null && root.left.right == null) ans+= root.left.val;
            else ans+= sumOfLeftLeaves(root.left);
        }
        ans+= sumOfLeftLeaves(root.right);
        return ans;
    }
```

## iterative

构造一个队列 `Queue<TreeNode> q = new LinkedList<TreeNode>();`

```java
 public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        int ans = 0;
        while (!q.isEmpty()){
            TreeNode curr = q.poll();
            if (curr.left != null) {
                if (curr.left.left == null && curr.left.right == null) ans += curr.left.val;
                else q.add(curr.left);
            }
            if (curr.right != null) q.add(curr.right);
        }
        return ans;
    }
```
