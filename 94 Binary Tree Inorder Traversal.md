# 94. Binary Tree Inorder Traversal

## 题目

给定一个二叉树，返回它的中序 遍历。

**示例:**
```java
输入: [1,null,2,3]

   1
    \
     2
    /
   3

输出: [1,3,2]
```
**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？

## 解法

### 递归

写一个inOrder的递归函数。时间复杂度O(n)，空间复杂度在树退化成链时达到O(n)，

```java
public void inOrder(List<Integer> list, TreeNode root){
        if (root == null) return;
        if (root.left != null) inOrder(list, root.left);
        list.add(root.val);
        if (root.right!=null) inOrder(list, root.right);
    }
```

### 迭代

先把左子树循环入栈。

```java
 public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        //inOrder(list, root);

        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        while (!stack.isEmpty() || curr != null){
            while (curr != null) {
                stack.push(root);
                curr = curr.left;
            }
            curr = stack.pop();
            list.add(root.val);
            curr = curr.right;
        }
        return list;
    }
```

### Morris迭代

能不能将迭代的空间复杂度降为O(1)?

Morris迭代通过找当前节点中序遍历的前驱节点，修改前驱节点的右子树用于判断当前节点的左子树是否被遍历完成，从而降低了空间复杂度。

算法过程：  
假设遍历到当前节点 curr  
1. 如果curr没有左子树，直接加入列表去遍历右子树。
2. 如果curr有左子树  
    2.1. 寻找curr左子树中最右的节点，即中序遍历中curr的前一个节点prev，记prev的右孩子为curr，表示开始遍历左子树。  
    2.1. 如果发现prev的右孩子已经被标记为curr那么表示这颗左子树已经遍历完成。断开连接，遍历curr的右子树。

```java
  public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        //inOrder(list, root);

        TreeNode prev = null;
        TreeNode curr = root;
        while (curr != null){
           if (curr.left == null){
               list.add(curr.val);
               curr = curr.right;
           } else {
               prev = curr.left;
               while (prev.right != null && prev.right != curr){
                   prev = prev.right;
               }

               if (prev.right == null){
                   prev.right = curr;
                   curr = curr.left;
               } else {
                   prev.right = null;
                   list.add(curr.val);
                   curr = curr.right;
               }
           }
        }
        return list;
    }
```

