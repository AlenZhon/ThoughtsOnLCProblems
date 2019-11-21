# 976. Largest Perimeter Triangle

## 题目

给定一个数组，从数组中选取三个数，使其围成的三角形周长最大。如果所有数字都无法围成三角形则返回0.

>Given an array A of positive lengths, return the largest perimeter of a triangle with non-zero area, formed from 3 of these lengths.
>
>If it is impossible to form any triangle of non-zero area, return 0.
>
>**Example 1:**
>
>>Input: [2,1,2]  
>>Output: 5
>
>**Example 2:**
>
>>Input: [1,2,1]  
>>Output: 0
>
>**Example 3:**
>
>>Input: [3,2,3,4]
>>Output: 10
>
>**Example 4:**
>
>>Input: [3,6,2,3]  
>>Output: 8
>
>**Note:**
>
> - `3 <= A.length <= 10000`
> - `1 <= A[i] <= 10^6`

## 解法

要构成三角形，需要两边之和大于第三边。排序完事。时间复杂度是排序的O(nlogn)，空间复杂度也根据built-in的排序决定。

```java
public int largestPerimeter(int[] A) {
        Arrays.sort(A);
        for (int i = A.length - 3; i >= 0; i--)
            if (A[i] + A[i + 1] > A[i + 2]) return A[i] + A[i+1] +A[i+2];
        return 0;
    }
```
