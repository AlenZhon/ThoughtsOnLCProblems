# 977. Squares of a Sorted Array

## 题目

给定一个非降序排列的数组A，数组元素范围在`[-10000,10000]`，将每个元素平方后非降序排列，构成一个新的数组，返回此数组。

>Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.
>
>**Example 1:**
>
>>Input: [-4,-1,0,3,10]  
>>Output: [0,1,9,16,100]
>
>**Example 2:**
>
>>Input: [-7,-3,2,3,11]  
>>Output: [4,9,9,49,121]
>
>Note:
>
> - 1 <= A.length <= 10000
> - -10000 <= A[i] <= 10000
> - A is sorted in non-decreasing order.

## 解法

two-pointers解决问题。指针从两端向中间靠拢，新数组ret从后向前填充。时间复杂度O(n)，空间O(1)（ret数组不算的话）。

```java
public int[] sortedSquares(int[] A) {
        int i = 0, j = A.length - 1;
        int[] ret = new int[A.length];
        for (int k = A.length - 1; k>=0; k--){
            int sqri = A[i] * A[i];
            int sqrj = A[j] * A[j];
            if (sqri > sqrj) {
                ret[k] = sqri;
                i++;
            } else {
                ret[k] = sqrj;
                j--;
            }
        }
        return ret;
    }
```
