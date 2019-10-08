# 107. Binary Tree Level Order Traversal II

## 题目

给定二叉树，层序遍历并返回从叶子节点到根节点的值。

>Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).
>
>For example:  
>Given binary tree `[3,9,20,null,null,15,7]`,
>
>>&nbsp;&nbsp;&nbsp;&nbsp;3  
>>&nbsp;&nbsp;&nbsp;/ \  
>>&nbsp;&nbsp;9  20  
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/  \  
>>&nbsp;&nbsp;&nbsp;15   7  
>
>return its bottom-up level order traversal as:
>
>>[  
>>&nbsp;&nbsp;[15,7],  
>>&nbsp;&nbsp;[9,20],  
>>&nbsp;&nbsp;[3]  
>>]

## 解法

和 *429. N-ary Tree Level Order Traversal* 想法相似，将`List<List<Integer>>`传入递归函数，每次添加元素时计算其应该添加在第几个`List`里。使用`add(int index, E elment)`增加新的`List`

```java
public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ret = new LinkedList<>();
        if (root == null) return ret;
        levelOrder(root, 0, ret);
        return ret;
    }

    private void levelOrder(TreeNode node, int depth, List<List<Integer>> ret) {
        if (ret.size() <= depth) ret.add(0, new LinkedList<Integer>());
        ret.get(ret.size() - depth - 1).add(node.val);
        if (node.left != null) levelOrder(node.left, depth + 1, ret);
        if (node.right != null) levelOrder(node.right, depth + 1, ret);
    }
```
