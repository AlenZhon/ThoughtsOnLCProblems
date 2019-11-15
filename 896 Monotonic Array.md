# 896. Monotonic Array

## 题目

给定一个数组，判断这个数组是否是单调的（单调增或单调减）

>An array is monotonic if it is either monotone increasing or monotone decreasing.
>
>An array A is monotone increasing if for all `i <= j, A[i] <= A[j]`.  An array A is monotone decreasing if for all `i <= j, A[i] >= A[j]`.
>
>Return true if and only if the given array A is monotonic.
>
>**Example 1:**
>
>>Input: [1,2,2,3]  
>>Output: true  
>
>**Example 2:**
>
>>Input: [6,5,4,4]  
>>Output: true
>
>**Example 3:**
>
>>Input: [1,3,2]  
>>Output: false
>
>**Example 4:**
>
>>Input: [1,2,4,5]  
>>Output: true
>
>**Example 5:**
>
>>Input: [1,1,1]  
>>Output: true
>
>**Note:**
>
> - `1 <= A.length <= 50000`
> - `-100000 <= A[i] <= 100000`

## 解法

时间复杂度O(N)，空间O(1)的题目。

### two-pass

可以走两轮循环，分别判断数列是单调增/单调减，满足一个则返回true。

```java
public boolean isMonotonic(int[] A) {
        return increasing(A) || decreasing(A);
    }

    public boolean increasing(int[] A) {
        for (int i = 0; i < A.length - 1; ++i)
            if (A[i] > A[i+1]) return false;
        return true;
    }

    public boolean decreasing(int[] A) {
        for (int i = 0; i < A.length - 1; ++i)
            if (A[i] < A[i+1]) return false;
        return true;
    }
```

### one-pass

把上面的两轮循环合并成一个。初始化两个变量分别表示增和减均为true。如果是单调数列，这两个布尔型变量只会改变其中之一，只有非单调数列中才会出现既增又减的情况。

```java
public boolean isMonotonic(int[] A) {
        if (A.length == 1 ) return true;
        boolean increase = true, decrease = true;
        for (int i = 1; i< A.length; i++) {
            if (A[i] == A[i - 1]) continue;
            if (A[i] > A[i - 1])
                decrease = false;
            else
                increase = false;
        }
        return increase || decrease;
    }
```
