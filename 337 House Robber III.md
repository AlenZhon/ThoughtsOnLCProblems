# 337. House Robber III

## 题目

>The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.
>
>Determine the maximum amount of money the thief can rob tonight without alerting the police.
>
>**Example 1:**
>
>>```java
>>Input: [3,2,3,null,3,null,1]  
>>
>>     3
>>    / \
>>   2   3
>>    \   \
>>     3   1
>>
>>Output: 7
>>Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
>
>**Example 2:**
>
>>```java
>>Input: [3,4,5,1,3,null,1]  
>>
>>     3
>>    / \
>>   4   5
>>  / \   \
>> 1   3   1
>>
>>Output: 9
>>Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
>>```

## 解法

### recursive

1.用一个HashMap存储当前节点为根节点时的最佳方案。

```java
    private Map<TreeNode, Integer> mem = new HashMap<>();

    public int rob(TreeNode root) {
        if(root == null) {
            return 0;
        }

        if(mem.containsKey(root)) {
            return mem.get(root);
        }

        int sum1 = 0;
        int sum2 = root.val;
        if (root.left != null) {
            sum1+=rob(root.left);
            sum2+=rob(root.left.left);
            sum2+=rob(root.left.right);
        }
        if (root.right != null) {
            sum1+=rob(root.right);
            sum2+=rob(root.right.left);
            sum2+=rob(root.right.right);
        }

        Integer result = Math.max(sum1, sum2);
        mem.put(root, result);

        return result;
    }
```

2.另一种方法。

```java
public int rob(TreeNode root) {
        if (root == null) return 0;
        int[] res = dfs(root);
        return Math.max(res[0],res[1]);
    }
    public int[] dfs(TreeNode root) {
        if (root == null) {
            return new int[]{0,0};
        }
        int[] left = dfs(root.left);
        int[] right = dfs(root.right);
        int[] cur = new int[2];
        cur[0] = Math.max(left[0],left[1]) + Math.max(right[0],right[1]);
        cur[1] = root.val + left[0] + right[0];
        return cur;
    }
```
