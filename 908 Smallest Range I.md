# 908. Smallest Range I

## 题目

给定一个数组A，对于每个数组元素 `A[i]` 我们可以上下浮动K以内的值，从而得到新的数组B。经过这一顿操作，求数组B中最大值和最小值之差值的最小可能值。

>Given an array A of integers, for each integer `A[i]` we may choose any x with `-K <= x <= K`, and add x to `A[i]`.
>
>After this process, we have some array B.
>
>Return the smallest possible difference between the maximum value of B and the minimum value of B.
>
>**Example 1:**
>
>>Input: A = `[1]`, K = 0  
>>Output: 0  
>>Explanation: B = `[1]`  
>
>**Example 2:**
>
>>Input: A = `[0,10]`, K = 2  
>>Output: 6  
>>Explanation: B = `[2,8]`
>
>**Example 3:**
>
>>Input: A = `[1,3,6]`, K = 3  
>>Output: 0  
>>Explanation: B = `[3,3,3]` or B = `[4,4,4]`
>
>**Note:**
>
> - `1 <= A.length <= 10000`
> - `0 <= A[i] <= 10000`
> - `0 <= K <= 10000`

## 解法

读完题就知道解法系列。找到数列A原本的最大值和最小值min和max，用`2*K`将他们的距离拉近。如果`(max - min) - 2 * K <= 0`，那么他们之间的最小差值肯定是0.

时间复杂度O(N)，空间复杂度O(1)。

```java
public int smallestRangeI(int[] A, int K) {
        int min = 10001, max = -1;
        if (A.length == 1) return 0;
        for (int a : A){
            if (min > a) min = a;
            if (max < a) max = a;
        }
        int ans = (max - min) - 2 * K;
        return ans > 0 ? ans : 0;
    }
```
