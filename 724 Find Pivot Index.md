# 724. Find Pivot Index

## 题目

如果对于数组中的元素，其左边元素之和与其右边元素之和相等，则定义该元素下标为 pivot index。给定数组，找出数组中的 pivot index，如果有多个满足条件的答案，返回最靠左边的。如果无解，返回-1.

>Given an array of integers nums, write a method that returns the "pivot" index of this array.
>
>We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.
>
>If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.
>
>**Example 1:**
>
>>Input:  
>>nums = `[1, 7, 3, 6, 5, 6]`  
>>Output: 3  
>>Explanation:  
>>The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
>>Also, 3 is the first index where this occurs.
>
>**Example 2:**
>
>Input:  
>>nums = `[1, 2, 3]`  
>>Output: -1  
>>Explanation:  
>>There is no index that satisfies the conditions in the problem statement.
>
>**Note:**
>
> - The length of `nums` will be in the range `[0, 10000]`.
> - Each element `nums[i]` will be an integer in the range `[-1000, 1000]`.

## 解法

题目不难理解，但是为什么数组的开头元素和结尾元素也算在内？个人觉得对于nums[0]来说，它左边元素之和（或nums[nums.length - 1]的右边元素之和）应该是没有意义的(null)。在这里定义为0了。

```java
public int pivotIndex(int[] nums) {
        if (nums.length <=2) return -1;
        int left = 0, sum = 0;
        for (int num : nums) sum += num;
        for (int i = 0; i < nums.length; i++) {
            if (2 * left == sum - nums[i]) return i;
            left += nums[i];
        }
        return -1;
    }
```

时间复杂度O(n)， 空间O(1)。
