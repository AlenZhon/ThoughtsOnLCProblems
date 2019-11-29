# 1018. Binary Prefix Divisible By 5

## 题目

用一个数组A存储0或1。`N_i`表示从`A[0]-A[i]`组成的二进制数的对应十进制。  
返回一个`List<Boolean>`如果`N_i`能被5整除则list[i]为真，反之为假。

>Given an array A of 0s and 1s, consider `N_i`: the i-th subarray from `A[0] to A[i]` interpreted as a binary number (from most-significant-bit to least-significant-bit.)
>
>Return a list of booleans `answer`, where `answer[i]` is true if and only if `N_i` is divisible by 5.
>
>**Example 1:**
>
>>Input: [0,1,1]  
>>Output: [true,false,false]  
>>Explanation:  
>>The input numbers in binary are 0, 01, 011; which are 0, 1, and 3 in base-10.  Only the first number is divisible by 5, so answer[0] is true.
>
>**Example 2:**
>
>>Input: [1,1,1]  
>>Output: [false,false,false]  
>
>**Example 3:**
>
>>Input: [0,1,1,1,1,1]  
>>Output: [true,false,false,false,true,false]
>
>**Example 4:**
>
>>Input: [1,1,1,0,1]  
>>Output: [false,false,false,false,false]
>
>**Note:**
>
> - 1 <= A.length <= 30000
> - A[i] is 0 or 1

## 解法

实际上，如果 N_i = x，那么 N_(i+1) = 2 * x + A[i+1]，可以迭代判断x 是不是5的倍数。考虑到A的长度肯定会溢出Integer的范围，所以用x存储每次迭代后的余数。

```java
public List<Boolean> prefixesDivBy5(int[] A) {
        List<Boolean> ret = new ArrayList<>();
        int x = 0;
        for (int i = 0; i < A.length; i++){
            x = 2 * x + A[i];
            if (x % 5 == 0) ret.add(true);
            else ret.add(false);
            x %=5;
        }
        return ret;
    }
```

时间复杂度O(A.length)，空间复杂度O(1)(不把ret算在内的话)。
