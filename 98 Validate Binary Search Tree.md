# 98. Validate Binary Search Tree

## 题目

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

    节点的左子树只包含小于当前节点的数。
    节点的右子树只包含大于当前节点的数。
    所有左子树和右子树自身必须也是二叉搜索树。
```java
示例 1:

输入:
    2
   / \
  1   3
输出: true

示例 2:

输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```

## 解法

### 迭代

在中序遍历的时候判断prev节点是否小于当前节点即可。时间复杂度O(n)，空间复杂度O(n)。

```java
public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        long prevVal = Long.MIN_VALUE;
        while (curr != null || !stack.isEmpty()){
           while (curr != null){
               stack.push(curr);
               curr = curr.left;
           }
           curr = stack.pop();
           if (curr.val <= prevVal){
               return false;
           }
           prevVal = curr.val;
           curr = curr.right;
        }
        return true;
    }
```

### 递归

用上下界去框住子树的取值范围。当根节点时上下界为 +INF和-INF。时间复杂度为O(n)，空间复杂度递归栈空间在树退化成一条链时为最坏情况O(n)。

```java
 public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean isValidBST(TreeNode root, long left, long right){
        if (root == null) {
            return true;
        } 
        if (root.val <= left || root.val >= right){
            return false;
        }
        return isValidBST(root.left, left, root.val) && isValidBST(root.right, root.val, right);
    }
```