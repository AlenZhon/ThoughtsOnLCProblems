# 922. Sort Array By Parity II

## 题目

非负整数数组，恰巧一半元素为奇数，另一半偶数。要求将奇数元素放在奇数位上，偶数元素放在偶数位上。奇偶内部的顺序不做要求。

>Given an array A of non-negative integers, half of the integers in A are odd, and half of the integers are even.
>
>Sort the array so that whenever A[i] is odd, i is odd; and whenever A[i] is even, i is even.
>
>You may return any answer array that satisfies this condition.
>
>**Example 1:**
>
>>Input: [4,2,5,7]  
>>Output: [4,5,2,7]  
>>Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
>
>**Note:**
>
> - `2 <= A.length <= 20000`
> - `A.length % 2 == 0`
> - `0 <= A[i] <= 1000`

## 解法

还是two-pointers。每次移两格直到两个指针都到了对面的尽头。时间复杂度O(n)，空间复杂度O(1)

```java
public int[] sortArrayByParityII(int[] A) {
        int  i = 0, j = A.length - 1;
        while (i <= A.length - 2 && j >= 1){
            if (A[i] % 2 == 1 && A[j] % 2 == 0){
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
            while (i <= A.length - 2 && A[i] % 2 == 0) i+=2;
            while (j >= 1  &&  A[j] % 2 == 1) j -= 2;
        }
        return A;
    }
```

根据题目，如果数列的偶数位上都是偶数，那么奇数位上必然都是奇数。从数列的同一边开始遍历（如左侧），那么指针i左侧的偶数位已经排好，指针j右侧的奇数元素为待判断的。时间复杂度和空间复杂度和上面的方法相同。

```java
public int[] sortArrayByParityII(int[] A) {
        int j = 1;
        for (int i = 0; i < A.length; i += 2)
            if (A[i] % 2 == 1) {
                while (A[j] % 2 == 1)
                    j += 2;

                // Swap A[i] and A[j]
                int tmp = A[i];
                A[i] = A[j];
                A[j] = tmp;
            }

        return A;
    }
```

相关的题目在 *905 Sort Array By Parity* 。
