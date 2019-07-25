# 136. Single Number

## 题目描述

给定非空数组，数组元素除了一个元素只出现一次，其他均成对出现。找出那个单独的元素。尝试设计一个不使用extra memory的算法。

>Given a non-empty array of integers, every element appears twice except for one. Find that single one.
>
>**Note:**
>
>Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
>
>Example 1:
>
>**Input:** [2,2,1]  
>**Output:** 1
>
>Example 2:
>
>**Input:** [4,1,2,1,2]  
>**Output:** 4

## 怎么解的

异或运算能够将成对出现的元素都算成0。如`4^4` (即4 XOR 4)，就是100^100 = 0。最后留下来的必定是那个只出现一次的元素。

既然不消耗额外存储空间，那就用nums[0]来反复计算了。

```java
public int singleNumber(int[] nums) {
        for (int i = 1; i < nums.length; i++)
            nums[0] = nums[0] ^ nums[i];
        return nums[0];
    }
```

时间复杂度O(n)。  
然而Leetcode运行时间1ms，仅打败了50%的Java Online Submission？点进去看0ms的Submission是申请了一个`int res`来存运算结果最后返回res。
