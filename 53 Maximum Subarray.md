# 53 Maximum Subarray

## 题目描述

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

>**Example**:
>
>**Input:** [-2,1,-3,4,-1,2,1,-5,4],  
>**Output:** 6  
>**Explanation:** [4,-1,2,1] has the largest sum = 6.

## 怎么解

2层for暴力循环时间复杂度O(n^2),肯定是不行的。

采用动态规划的思想，时间复杂度O(n)。

```java
 public int maxSubArray(int[] nums) {
        int max = nums[0],tempmax = nums[0];
        for (int i= 1; i< nums.length; i++) {
            tempmax = Math.max(tempmax + nums[i], nums[i]);
            max  = Math.max(max, tempmax);
        }
        return max;
    }
```

## Notes

>**Follow up**  
>If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

分治策略将问题转化为从如下三种情况中挑选最大子数列之和：

1. 最大子数列处于`mid`左半边。
2. 最大子数列处于`mid`右半边。
3. 最大子数列在`left`和`right`中间，跨过了`mid`。

时间复杂度的递推公式： T(n) = 2* T(n / 2) + O(n)
因此时间复杂度为O(nlog_{2} n)

```java
public class Solution {//divdie and conquer
    public int maxSubArray(int[] nums) {
        return Subarray(nums, 0 ,nums.length -1 );
    }
    public int Subarray(int[] A,int left, int right){
        if(left == right){return A[left];}
        int mid = left + (right - left) / 2;
        int leftSum = Subarray(A,left,mid);// left part
        int rightSum = Subarray(A,mid+1,right);//right part
        int crossSum = crossSubarray(A,left,right);// cross part

        //following if condition will return middlesum if lost the "=" under the conditon of leftsum = rightsum, which may be problematic if leftsum = rightsum < middlesum.
        //for example: [-1, -1, -2, -2]
        if(leftSum >= rightSum && leftSum >= crossSum){// left part is max
            return leftSum;
        }
        if(rightSum >= leftSum && rightSum >= crossSum){// right part is max
            return rightSum;
        }
        return crossSum; // cross part is max
    }
    public int crossSubarray(int[] A,int left,int right){
        int leftSum = Integer.MIN_VALUE;
        int rightSum = Integer.MIN_VALUE;
        int sum = 0;
        int mid = left + (right - left) / 2;
        for(int i = mid; i >= left ; i--){
            sum = sum + A[i];
            if(leftSum < sum){
                leftSum = sum;
            }
        }
        sum = 0;
        for(int j = mid + 1; j <= right; j++){
            sum = sum + A[j];
            if(rightSum < sum){
                rightSum = sum;
            }
        }
        return leftSum + rightSum;
    }
}
```
