# 257. Binary Tree Paths

## 题目

>Given a binary tree, return all root-to-leaf paths.
>
>Note: A leaf is a node with no children.
>
>**Example:**
>
>Input:
>
>>&nbsp;&nbsp;&nbsp;1  
>&nbsp;&nbsp;/&nbsp;\  
>&nbsp;2&nbsp;&nbsp;3  
>&nbsp;&nbsp;\  
>&nbsp;&nbsp;5
>
>Output: ["1->2->5", "1->3"]
>
>Explanation: All root-to-leaf paths are: 1->2->5, 1->3

## 解法

就是一个DFS。

```java
 public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList<String>();
        if (root != null) dfs(root, "", res);
        return res;
    }

    private void dfs(TreeNode root, String s, List<String> list) {
        if (root.left == null && root.right == null) list.add(s + root.val);
        if (root.left != null) dfs(root.left, s + root.val +"->", list);
        if (root.right != null) dfs(root.right, s + root.val +"->", list);
    }
```

好奇StringBuilder对字符串拼接在Leetcode OJ上的运行效果。然而若是直接将上面程序的String类型改成StringBuilder时，发现示例运行结果是`["1->2->5","1->2->51->3"]`。看来在递归调用dfs()时StringBuilder始终指向同一个引用。

所以需要在每次递归调用前暂存StringBuilder

```java
public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList<String>();
        if (root != null) dfs(root, new StringBuilder(), res);
        return res;
    }

    private void dfs(TreeNode root, StringBuilder s, List<String> list) {
        if (root.left == null && root.right == null) {
            s.append(root.val);
            list.add(s.toString());
        }
        if (root.left != null) {
            String temp = s.toString();
            s.append(root.val).append("->");
            dfs(root.left, s, list);
            s = new StringBuilder(temp);
        }
        if (root.right != null) {
            String temp = s.toString();
            s.append(root.val).append("->");
            dfs(root.right, s, list);
            s = new StringBuilder(temp);
        }
    }
```

OJ的运行时间没有太大差别，都是1ms.
