# 559. Maximum Depth of N-ary Tree

## 题目

给定一个N叉树，求它的最大深度（根节点到最远叶节点的长度）。

>Given a n-ary tree, find its maximum depth.
>
>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
>
>For example, given a 3-ary tree:
>
>```java
>         1  
>       / | \  
>      2  3  4
>     /  
>    5
>```
>
>We should return its max depth, which is 3.

## 解法

水题。recursive时间复杂度O(n), 空间O(n)

```java
public int maxDepth(Node root) {
        if (root == null) return 0;
        int currMax = 0;
        for (Node node : root.children)
            currMax = Math.max(currMax, maxDepth(node));
        return 1 + currMax;
    }
```

iterative 使用队列存储待处理的节点。时间复杂度O(n),空间O(n)

```java
public int maxDepth(Node root) {
        if(root == null) return 0;
    int depth = 0;
    Queue<Node> queue = new LinkedList<Node>();
    queue.offer(root);
    while(!queue.isEmpty()) {
      int n = queue.size();
      for(int i = 0; i < n; i++) {
        root = queue.poll();
        for(Node node : root.children) {
          queue.offer(node);
        }
      }
      depth++;
    }
    return depth;
}
```
