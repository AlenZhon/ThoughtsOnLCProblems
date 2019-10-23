# 643. Maximum Average Subarray I

## 题目

给定一个数组和长度k，求出数组中连续k个数的最大平均值。

>Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.
>
>Example 1:
>
>>Input: `[1,12,-5,-6,50,3]`, k = 4  
>>Output: 12.75  
>>Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
>
>**Note:**
>
> - 1 <= k <= n <= 30,000.
> - Elements of the given array will be in the range `[-10,000, 10,000]`.

## 解法

Straight-forward. 构造一个长度为k的滑动窗口，每次向前滑动一格。保存滑动窗口的最大平均值。时间复杂度O(n) 空间O(1)。

```java
public double findMaxAverage(int[] nums, int k) {
        double ret = Integer.MIN_VALUE, sum = 0;
        for (int j = 0; j< k; j++)
            sum += nums[j];
        ret = sum;
        for (int i = k; i < nums.length; i++) {
            sum += (nums[i] - nums[i - k]);
            ret = Math.max(ret, sum);
        }
        return ret / k;
    }
```
