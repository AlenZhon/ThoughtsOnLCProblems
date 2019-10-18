# 589. N-ary Tree Preorder Traversal

## 题目

实现一个N叉树的前序遍历。

**Note:** 递归方法比较简单，尝试使用非递归方法去做。

## 解法

### 递归

没什么好说的。时间复杂度O(n)，空间复杂度O(n)

```java
public List<Integer> preorder(Node root) {
        List<Integer> ret = new ArrayList<>();
        preOrder(root, ret);
        return ret;
    }
    private void preOrder(Node node, List<Integer> list){
        if (node == null) return;
        list.add(node.val);
        for (Node child : node.children) preOrder(child, list);
        return;
    }
```

如果使用非递归的方法，则先入先出的队列适合层序遍历。利用栈的后入先出的特点，将当前节点的children列表翻转并依次压栈，则越靠近栈顶的元素越是在树的左下角。

查了查怎么样翻转List，用了`Collections.reverse(list)`。实际上用一个for循环从后向前读也可。

```java
public List<Integer> preorder(Node root) {
        List<Integer> ret = new ArrayList<>();
        Stack<Node> s = new Stack<>();
        if (root != null) s.push(root);
        Node curr;
        while (!s.isEmpty()) {
            curr = s.pop();
            ret.add(curr.val);
            //List<Node> child = curr.children;
            //Collections.reverse(child);
            //for (Node n : child) s.push(n);
            for (int i = curr.children.size() - 1; i>=0; i--)
                s.push(curr.children.get(i));
        }
        return ret;
    }
```

第一次提交没有对root做空指针判断， 报Runtime空指针错误。写粗了。
