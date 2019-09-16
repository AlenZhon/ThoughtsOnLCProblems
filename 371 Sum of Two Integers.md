# 371. Sum of Two Integers

## 题目

给定两个整数，要求不使用(+) (-)运算符的情况下求出两数之和。

>Calculate the sum of two integers a and b, but you are **not allowed** to use the operator `+` and `-`.
>
>**Example 1:**
>
>>Input: a = 1, b = 2  
>>Output: 3
>
>**Example 2:**
>
>>Input: a = -2, b = 3  
>>Output: 1

## 解法

既然不能使用加和减，回忆大计基内容自然想到补码相加。

尝试测试例发现原位相加遵循 `a XOR b`，进位遵循`a  AND b`。

```java
 public int getSum(int a, int b) {
        if(b == 0) return a;
        int carry = (a & b) << 1;
        int sum = a ^ b;
        return getSum(sum, carry);
    }
```
