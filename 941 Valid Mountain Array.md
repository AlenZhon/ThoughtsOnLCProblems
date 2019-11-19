# 941. Valid Mountain Array

## 题目

判断一个数组是否先严格单调增，再严格单调降，形成一个Mountain Array。

>Recall that A is a mountain array if and only if:
>
> - `A.length >= 3`
> - There exists some i with 0 < i < A.length - 1 such that:
>- - `A[0] < A[1] < ... A[i-1] < A[i]`
>- - `A[i] > A[i+1] > ... > A[A.length - 1]`
>
>**Example 1:**
>
>>Input: [2,1]  
>>Output: false  
>
>**Example 2:**
>
>>Input: [3,5,5]  
>>Output: false  
>
>**Example 3:**
>
>>Input: [0,3,2,1]  
>>Output: true
>
>**Note:**
>
> - 0 <= A.length <= 10000
> - 0 <= A[i] <= 10000

## 解法

水到。时间复杂度O(n)，空间O(1)。找到非严格单调增的第一个点，判断之后是不是单调降。

```java
public boolean validMountainArray(int[] A) {
        if (A.length < 3) return false;
        int i = 1;
        while (i < A.length && A[i] > A[i - 1]) i++;
        if (i == 1 || i == A.length) return false;
        while (i < A.length) {
            if (A[i] >= A[i - 1]) return false;
            i++;
        }
        return true;
    }
```
