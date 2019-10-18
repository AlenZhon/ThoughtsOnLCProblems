# 590. N-ary Tree Postorder Traversal

## 题目

实现N叉树的后序遍历。

**Note:** 递归解法比较简单，考虑使用非递归解法解决。

## 解法

先上一个递归解法。

```java
public List<Integer> postorder(Node root) {
        List<Integer> ret = new ArrayList<>();
        postOrder(root, ret);
        return ret;
    }
    private void postOrder(Node node, List<Integer> list) {
        if (node == null) return;
        for (Node child: node.children )
            postOrder(child, list);
        list.add(node.val);
    }
```

对于非递归写法，由于后序遍历为： `node.leftmostChild -> ... -> node.rightmostChild -> node`， 是`node -> node.rightmostChild -> .. node.leftmostChild` 的翻转。child的先右后左可以通过栈的后入先出性质实现。

```java
public List<Integer> postorder(Node root) {
        List<Integer> ret = new ArrayList<>();
        Stack<Node> s = new Stack<>();
        if (root != null) s.push(root);
        Node curr;
        while (!s.isEmpty()) {
            curr = s.pop();
            ret.add(curr.val);
            for (Node child : curr.children)
                s.push(child);
        }
        Collections.reverse(ret);
        return ret;
    }
```
