# 653. Two Sum IV - Input is a BST

## 题目

给定二叉搜索树和一个整数k，判断能否在BST中找到两个数，使得这两个数之和等于k.

>Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.
>
>Example 1:
>
>>Input:
>>
>>```java
>>     5
>>    / \
>>   3   6
>>  / \   \
>> 2   4   7
>>
>>Target = 9
>>```
>>
>>Output: True
>
>Example 2:
>
>>Input:
>>
>>```java
>>     5
>>    / \
>>   3   6
>>  / \   \
>> 2   4   7
>>
>>Target = 28
>>```
>>
>>Output: False

## 解法

递归加HashSet。

```java
 public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<>();
        return helper(root, k, set);
    }

    private boolean helper(TreeNode root, int k , Set<Integer> s) {
        if (root == null) return false;
        if (s.contains(k - root.val)) return true;
        s.add(root.val);
        return helper(root.left, k, s) || helper(root.right, k , s);
    }
```

时间复杂度和空间复杂度都在最坏的情况下达到O(n)。

使用BST的性质，先中序遍历构造有序数列，再用two-pointer遍历数列。时间复杂度：中序遍历时的O(n),two pointer时O(n)，空间复杂度O(n)

```java
public boolean findTarget(TreeNode root, int k) {
        List<Integer> nums = new ArrayList<>();
        inOrder(root, nums);
        Integer[] array = nums.toArray(new Integer[nums.size()]);
        int left = 0, right = array.length -1;
        while (left < right) {
            int sum = array[left] + array[right];
            if (sum == k) return true;
            else if (sum < k) left++;
            else right--;
        }
        return false;
    }
    private void inOrder(TreeNode root, List<Integer> list) {
        if (root == null) return;
        inOrder(root.left, list);
        list.add(root.val);
        inOrder(root.right, list);
    }
```
