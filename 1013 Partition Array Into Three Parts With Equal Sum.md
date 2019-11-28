# 1013. Partition Array Into Three Parts With Equal Sum

## 题目

给定一个整数数组，判断是否能够找到两个下标`i, j (i + 1 < j)`，这两个下标将数组分成三部分，使得这三部分的和相等。如果这样的下标存在，返回true。返回false。

>Given an array A of integers, return true if and only if we can partition the array into three non-empty parts with equal sums.
>
>Formally, we can partition the array if we can find indexes `i+1 < j` with `(A[0] + A[1] + ... + A[i] == A[i+1] + A[i+2] + ... + A[j-1] == A[j] + A[j-1] + ... + A[A.length - 1])`
>
>**Example 1:**
>
>>Input: `[0,2,1,-6,6,-7,9,1,2,0,1]`  
>>Output: true  
>>Explanation: 0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
>
>**Example 2:**
>
>>Input: `[0,2,1,-6,6,7,9,-1,2,0,1]`  
>>Output: false
>
>**Example 3:**
>
>>Input: `[3,3,6,5,-2,2,5,1,-9,4]`  
>>Output: true  
>>Explanation: 3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
>
>**Note:**
>
> - 3 <= A.length <= 50000
> - -10000 <= A[i] <= 10000

## 解法

如果数组的三部分元素和相等，那么肯定数组元素之和`sum`能被三整除。two-pointer从首尾开始找元素下标，判断元素之和是否等于`sum / 3`。

时间复杂度O(N)，空间O(1)。

```java
public boolean canThreePartsEqualSum(int[] A) {
        int sum = 0;  //50000 * 10000 < INTEGER.MAX_VALUE
        for (int num : A)
            sum+= num;
        if (sum % 3 != 0) return false; // must be integer
        int sum3 = sum / 3, i = 0, j = A.length - 1;
        int leftsum =0, rightsum = 0;
        while (i < j && leftsum != sum3)
            leftsum += A[i++];
        if (leftsum != sum3) return false; // when i = j but still cant get leftsum
        while (i < j && rightsum != sum3)
            rightsum += A[j--];
        if (rightsum != sum3) return false;
        return true;
    }
```
