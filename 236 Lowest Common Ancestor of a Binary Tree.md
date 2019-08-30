# 236. Lowest Common Ancestor of a Binary Tree

## 题目

给定一个二叉树和其中的两个节点，找到这两个节点的LCA。允许一个节点同时是自己的前驱。

>Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
>
>According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (**where we allow a node to be a descendant of itself**).”
>
>Given the following binary tree:  root = [3,5,1,6,2,0,8,null,null,7,4]
>
>**Example 1:**
>>
>>Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1  
>>Output: 3  
>>Explanation: The LCA of nodes 5 and 1 is 3.
>
>**Example 2:**
>>
>>Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4  
>>Output: 5  
>>Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
>
>**Note:**
>
> - All of the nodes' values will be unique.
> - p and q are different and both values will exist in the binary tree.

## 解法

是 *#235* 的升级版，把二叉搜索树改成了二叉树，缺少了  *#235* 的关键解题性质。

### Recursive

看了讨论区，迭代解法的主要想法：

>If the current (sub)tree contains both p and q, then the function result is their LCA.  
>If only one of them is in that subtree, then the result is that one of them.  
>If neither are in that subtree, the result is `null`.

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root ==null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left == null && right == null) {
            return null;
        } else if (left != null && right != null) {
            return root;  
        }
        return left == null ? right : left;
    }
```

[思路](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solution/)里是用布尔返回值的函数做递归。

```java
  private TreeNode ans;

  public Solution() {
      // Variable to store LCA node.
      this.ans = null;
    }

  private boolean recurseTree(TreeNode currentNode, TreeNode p, TreeNode q) {
      // If reached the end of a branch, return false.
      if (currentNode == null) return false;

      // Left Recursion. If left recursion returns true, set left = 1 else 0
      int left = this.recurseTree(currentNode.left, p, q) ? 1 : 0;

      // Right Recursion
      int right = this.recurseTree(currentNode.right, p, q) ? 1 : 0;

      // If the current node is one of p or q
      int mid = (currentNode == p || currentNode == q) ? 1 : 0;

      // If any two of the flags left, right or mid become True
      if (mid + left + right >= 2) this.ans = currentNode;

      // Return true if any one of the three bool values is True.
      return (mid + left + right > 0);
  }

  public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
      // Traverse the tree
      this.recurseTree(root, p, q);
      return this.ans;
  }
```

时间复杂度和空间复杂度都是O(N)。

### Iterative

由于需要深度优先遍历，所以迭代的方法需要存储每个节点的前驱。

#### Algorithm

> - Start from the root node and traverse the tree.
> - Until we find p and q both, keep storing the parent pointers in a dictionary.
> - Once we have found both p and q, we get all the ancestors for p using the parent dictionary and add to a set called ancestors.
> - Similarly, we traverse through ancestors for node q. If the ancestor is present in the ancestors set for p, this means this is the first ancestor common between p and q (while traversing upwards) and hence this is the LCA node.

```java
class Solution {

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {

        // Stack for tree traversal
        Deque<TreeNode> stack = new ArrayDeque<>();

        // HashMap for parent pointers
        Map<TreeNode, TreeNode> parent = new HashMap<>();

        parent.put(root, null);
        stack.push(root);

        // Iterate until we find both the nodes p and q
        while (!parent.containsKey(p) || !parent.containsKey(q)) {

            TreeNode node = stack.pop();

            // While traversing the tree, keep saving the parent pointers.
            if (node.left != null) {
                parent.put(node.left, node);
                stack.push(node.left);
            }
            if (node.right != null) {
                parent.put(node.right, node);
                stack.push(node.right);
            }
        }

        // Ancestors set() for node p.
        Set<TreeNode> ancestors = new HashSet<>();

        // Process all ancestors for node p using parent pointers.
        while (p != null) {
            ancestors.add(p);
            p = parent.get(p);
        }

        // The first ancestor of q which appears in
        // p's ancestor set() is their lowest common ancestor.
        while (!ancestors.contains(q))
            q = parent.get(q);
        return q;
    }

}
```

时间复杂度和空间复杂度是O(N)。
