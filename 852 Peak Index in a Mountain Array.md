# 852. Peak Index in a Mountain Array

## 题目

一个长度不小于3的数列，如果存在某元素 `A[i]` 使得 `A[0] < A[1] < ... A[i] > A[i+1] > ... > A[n]` 成立，则称该数列为山数列(mountain Array)。 给定一个山数列，求满足条件的峰值下标i。

>Let's call an array A a mountain if the following properties hold:
>
> - `A.length >= 3`
> - There exists some `0 < i < A.length - 1` such that `A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]`
>
>Given an array that is definitely a mountain, return any `i` such that `A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]`.
>
>**Example 1:**
>
>>Input: [0,1,0]  
>>Output: 1
>
>**Example 2:**
>>
>>Input: [0,2,1,0]  
>>Output: 1
>
>**Note:**
>
> - `3 <= A.length <= 10000`
> - `0 <= A[i] <= 10^6`
> - `A` is a mountain, as defined above.

## 解法

典型的二分查找。比较mid和mid左右两边的元素大小，即可知道mid就是峰值，还是在峰值的左侧/右侧。时间复杂度O(log_2 N)，空间复杂度O(1)

```java
public int peakIndexInMountainArray(int[] A) {
        int left = 0, right = A.length - 1;
        while (left < right) {
            int mid = left + (right - left )/ 2;
            if (A[mid] > A[mid - 1] && A[mid] > A[mid + 1]) return mid;
            if (A[mid] > A[mid - 1] && A[mid] < A[mid + 1]) left = mid;
            if (A[mid] < A[mid - 1] && A[mid] > A[mid + 1]) right = mid;
        }
        return left;
    }
```
