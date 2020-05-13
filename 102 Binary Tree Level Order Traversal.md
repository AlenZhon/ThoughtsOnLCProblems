# 102. Binary Tree Level Order Traversal

## 题目

>给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。
>
>**示例：**  
>二叉树：[3,9,20,null,null,15,7],
>
>```java
>    3
>   / \
>  9  20
>    /  \
>   15   7
>```
>返回其层次遍历结果：
>
>[  
>  [3],  
>  [9,20],  
>  [15,7]  
>]

## 解法

### 递归

用一个helper函数做递归，维护当前遍历到的层数，进入一次递归就层数加一。

```java
public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new LinkedList<>();
        if (root == null) return ret;
        levelOrderHelper(root, 0, ret);
        return ret;
    }
    public void levelOrderHelper(TreeNode root, int height, List<List<Integer>> list){
        if (list.size() <= height) list.add(new LinkedList<Integer>());
        list.get(height).add(root.val);
        if (root.left != null) levelOrderHelper(root.left, height + 1, list);
        if (root.right != null) levelOrderHelper(root.right, height + 1, list);
    }
```

### 非递归

```java
public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        if (root == null) return ret;
        q.add(root);
        while (!q.isEmpty()){
            List<Integer> tmpList = new LinkedList<>();
            int count = q.size();
            while (count > 0) {
                TreeNode tmp = q.poll();
                tmpList.add(tmp.val);
                if (tmp.left != null) q.add(tmp.left);
                if (tmp.right != null) q.add(tmp.right);
                count--;
            }
            ret.add(tmpList);
        }
        return ret;
    }
```