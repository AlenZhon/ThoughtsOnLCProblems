# 1089. Duplicate Zeros

## 题目

给定一个固定长度的数组，将里面的0元素重复一次，其他元素向右移动。将上述操作在原数组In-place完成。

>Given a fixed length array arr of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.
>
>Note that elements beyond the length of the original array are not written.
>
>Do the above modifications to the input array in place, do not return anything from your function.
>
>**Example 1:**
>
>>Input: [1,0,2,3,0,4,5,0]  
>>Output: null  
>>Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]
>
>**Example 2:**
>
>>Input: [1,2,3]  
>>Output: null  
>>Explanation: After calling your function, the input array is modified to: [1,2,3]
>
>Note:
>
> - 1 <= arr.length <= 10000
> - 0 <= arr[i] <= 9

## 解法

既然是in-place，想一个不使用额外存储空间的方法。按照题目要求，新的数组长度应该为原始数组长度 + 0的个数。所以先统计0的个数，然后从后往前遍历，把元素向后挪动。

```java
public void duplicateZeros(int[] arr) {
        int zeros = 0;
        for (int a : arr)
            if (a == 0) zeros++;
        for (int i = arr.length - 1; i>=0 && zeros > 0 ; i--){
            if (arr[i] == 0) {
                zeros--;
                if (i + zeros < arr.length) arr[i + zeros] = 0;
                if (i + zeros + 1 < arr.length) arr[i + zeros + 1] = 0;
            } else if (i < arr.length - zeros) arr[i + zeros] = arr[i];
        }
    }
```

时间复杂度O(N)，空间复杂度O(1)。
