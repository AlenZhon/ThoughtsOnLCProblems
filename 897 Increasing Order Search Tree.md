# 897. Increasing Order Search Tree

## 题目

给定一棵二叉搜索树，中序遍历该树使其按序排列，所有节点形成一棵新的树。在这棵新树中，根节点是BST的最左下角的节点，并且新树中的每一个节点只有一个右子节点。节点的值各不相同且取值范围在`[0,1000]`。

>Given a binary search tree, rearrange the tree in in-order so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only 1 right child.
>
>**Example 1:**
>>
>>```java
>>Input: [5,3,6,2,4,null,8,1,null,null,null,7,9]
>>
>>        5
>>       / \
>>     3    6
>>    / \    \
>>   2   4    8
>>  /        / \
>> 1        7   9
>>
>>Output: [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
>>
>>
>> 1
>>  \
>>   2
>>    \
>>     3
>>      \
>>       4
>>        \
>>         5
>>          \
>>           6
>>            \
>>             7
>>              \
>>               8
>>                \
>>                 9  
>>```
>
>**Note:**
>
> - The number of nodes in the given tree will be between 1 and 100.
> - Each node will have a unique integer value from 0 to 1000.

## 解法

### inOrder

按照题目的意思中序遍历存入列表，然后再生成新的树。时间复杂度O(N)，空间复杂度O(N)。

```java
public TreeNode increasingBST(TreeNode root) {
        List<Integer> value = new ArrayList<Integer>();
        inOrder(root, value);
        TreeNode point = new TreeNode(0), curr = point;
        for (Integer val : value){
            curr.right = new TreeNode(val);
            curr = curr.right;
        }
        return point.right;
    }
    private void inOrder(TreeNode node, List<Integer> val){
        if (node == null) return;
        inOrder(node.left, val);
        val.add(node.val);
        inOrder(node.right, val);
    }
```

由于中序遍历一个BST肯定得到一个单调数列，并且题目明确说节点元素值各不相同，所以想把列表简化成`boolean[1001]`数组。改完一跑，在测试用例`[379,826]`前倒下了。标准输出是 `[826, null, 379]`， 我是 `[379, null, 826]` 。题目并没有说BST左下角就一定是整棵树里最小的元素？

## Relinking

在中序遍历的同时完成新树的生成。时间复杂度O(N)，空间复杂度变为O(H)。

```java
    private TreeNode curr;
    public TreeNode increasingBST(TreeNode root) {
        TreeNode point = new TreeNode(0);
        curr = point;
        inOrder(root);
        return point.right;
    }
    private void inOrder(TreeNode node){
        if (node == null) return;
        inOrder(node.left);
        node.left = null;
        curr.right = node;
        curr = node;
        inOrder(node.right);
    }
```
