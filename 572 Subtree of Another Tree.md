# 572. Subtree of Another Tree

## 题目

给定两棵二叉树`s,t`，判断`t`是否是s的子树。

>Given two non-empty binary trees s and t, check whether tree t has exactly the same structure and node values with a subtree of s. A subtree of s is a tree consists of a node in s and all of this node's descendants. The tree s could also be considered as a subtree of itself.
>
>**Example 1:**
>>
>>```java
>>Given tree s:
>>
>>     3
>>    / \
>>   4   5
>>  / \
>> 1   2
>>
>>Given tree t:
>>   4
>>  / \
>> 1   2
>>
>>Return true, because t has the same structure and node values with a subtree of s.
>
>**Example 2:**
>>
>>```java
>>Given tree s:
>>
>>     3
>>    / \
>>   4   5
>>  / \
>> 1   2
>>    /
>>   0
>>
>>Given tree t:
>>
>>   4
>>  / \
>> 1   2
>>
>>Return false.

## 解法

遍历s的每一个节点并看做根节点，然后用 *#100 same tree* 的方法判断该根节点构成的子树和t是否相同。

```java
public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null) return false;
        if (isSameTree(s, t)) return true;
        return isSubtree(s.left, t) || isSubtree(s.right, t);
    }

    private boolean isSameTree(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        return s.val == t.val && isSameTree(s.left, t.left) && isSameTree(s.right, t.right);
    }
```