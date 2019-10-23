# 637. Average of Levels in Binary Tree

## 题目

一个非空的二叉树，计算其每层节点的平均值。

>Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.
>
>Example 1:
>
>>Input:
>>
>>```java
>>    3
>>   / \
>>  9  20
>>    /  \
>>   15   7
>>```
>>
>>Output: `[3, 14.5, 11]`  
>>Explanation:  
>>The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return `[3, 14.5, 11]`.
>
>**Note:**
>
> - The range of node's value is in the range of 32-bit signed integer.

## 解法

### BFS

时间复杂度是O(n)，和二叉树结点个数有关。空间复杂度O(m)，和二叉树中单层最大节点数有关。

```java
public List<Double> averageOfLevels(TreeNode root) {
        List<Double> ret = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()) {
            int len = q.size();
            double sum = 0;
            for (int i = 0; i< len; i++){
                TreeNode node = q.poll();
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
                sum+= node.val;
            }
            ret.add(sum / len);
        }
        return ret;
    }
```

### DFS

```java
public List < Double > averageOfLevels(TreeNode root) {
        List < Integer > count = new ArrayList < > ();
        List < Double > res = new ArrayList < > ();
        average(root, 0, res, count);
        for (int i = 0; i < res.size(); i++)
            res.set(i, res.get(i) / count.get(i));
        return res;
    }
    public void average(TreeNode t, int i, List < Double > sum, List < Integer > count) {
        if (t == null)
            return;
        if (i < sum.size()) {
            sum.set(i, sum.get(i) + t.val);
            count.set(i, count.get(i) + 1);
        } else {
            sum.add(1.0 * t.val);
            count.add(1);
        }
        average(t.left, i + 1, sum, count);
        average(t.right, i + 1, sum, count);
    }
```

时间复杂度O(n)，整棵树只遍历一次。空间复杂度O(h)，和树的最大高度有关。
