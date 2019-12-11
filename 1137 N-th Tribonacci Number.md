# 1137. N-th Tribonacci Number

## 题目

类似Fibonacci数列，定义Tribonacci数列。

```java
T0 = 0
T1 = T2 = 1
T_(n+3) = T_(n+2) + T_(n+1) + T_(n)  
```

给定`n`求`T_n`。保证`T_n`在32位无符号整数范围内。

>The Tribonacci sequence Tn is defined as follows:
>
>>T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.
>
>Given n, return the value of Tn.
>
>**Example 1:**
>
>>Input: n = 4  
>>Output: 4  
>>Explanation:  
>>T_3 = 0 + 1 + 1 = 2  
>>T_4 = 1 + 1 + 2 = 4
>
>**Example 2:**
>
>>Input: n = 25  
>>Output: 1389537
>
>**Constraints:**
>
> - 0 <= n <= 37
> - The answer is guaranteed to fit within a 32-bit integer, ie. answer <= 2^31 - 1.

## 解法

根据hint提示，`n = 39`时`T_n`已经超出了`Integer`的范围。  
所以定义`new int[38]`，迭代求解即可。
