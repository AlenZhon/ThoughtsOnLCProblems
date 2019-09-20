# 429. N-ary Tree Level Order Traversal

## 题目

一个n叉树，返回它的层序遍历。
>Given an n-ary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
>
>**Note:**
>
> - The depth of the tree is at most 1000.
> - The total number of nodes is at most 5000.

## 解法

### Iterative

用了一个队列Queue维护每层需要访问的节点。每层节点的个数即为队列中当前元素的个数(关键)。时间和空间复杂度均为O(N)，N是节点个数。

```java
public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> ret = new LinkedList<>();
        if (root == null) return ret;
        Queue<Node> q = new LinkedList<Node>();
        q.add(root);
        while (!q.isEmpty()){
            List<Integer> temp = new ArrayList<Integer>();
            int len = q.size();
            for (int i=0; i< len; i++) {
                Node curr = q.poll();
                temp.add(curr.val);
                for (Node n : curr.children)
                    q.add(n);
            }
            ret.add(temp);
        }
        return ret;
    }
```

### Recursive

时间复杂度O(n), 空间复杂度O(n)

```java
public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> ret = new LinkedList<>();
        if (root ==null)return ret;
        levelOrder(root, 0, ret);
        return ret;
    }
    public void levelOrder(Node node, int depth, List<List<Integer>> res) {
        if (res.size() <= depth) res.add(new ArrayList<Integer>());
        res.get(depth).add(node.val);
        for (Node c : node.children) {
            if (c != null) levelOrder(c, depth + 1, res);
        }
    }
```
