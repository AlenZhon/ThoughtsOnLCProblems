# 674. Longest Continuous Increasing Subsequence

## 题目

给定一个数组，返回其中连续递增子数组的最大长度。

>Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).
>
>Example 1:
>
>>Input: [1,3,5,4,7]  
>>Output: 3  
>>Explanation: The longest continuous increasing subsequence is [1,3,5], its length is 3.  
>>Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4.  
>
>Example 2:
>
>>Input: [2,2,2,2,2]  
>>Output: 1  
>>Explanation: The longest continuous increasing subsequence is [2], its length is 1.  
>
>Note: Length of the array will not exceed 10,000.  

## 解法

Straight-forward. 保存当前递增数列的长度和之前的最大长度。

```java
public int findLengthOfLCIS(int[] nums) {
        if (nums.length == 0) return 0;
        int prevLen = 0, len = 1;
        for (int i = 1; i< nums.length; i++)
            if (nums[i] > nums[i-1])
                len++;
            else {
                prevLen = Math.max(prevLen, len);
                len = 1;
            }
        return Math.max(prevLen, len);
    }
```
