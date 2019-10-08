# 509. Fibonacci Number

## 题目

给定正整数N，计算第N个斐波那契数。数列从0,1开始。

>The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
>
>`F(0) = 0,   F(1) = 1`
>`F(N) = F(N - 1) + F(N - 2), for N > 1.`
>
>Given N, calculate F(N).
>
>Example 1:
>
>>Input: 2  
>>Output: 1  
>>Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
>
>Example 2:
>
>>Input: 3  
>>Output: 2  
>>Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
>
>Example 3:
>
>>Input: 4  
>>Output: 3  
>>Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
>
>**Note:**
>0 ≤ N ≤ 30.

## 解法

水题。给定了N的范围直接查数组就行。

要不然用两个变量迭代求解。

```java
public int fib(int N) {
        int prev0 = 0, prev1 = 1, ans = 0;
        if (N == 0) return prev0;
        if (N == 1) return prev1;
        for (int i = 2; i <=N; i++){
            ans = prev0 + prev1;
            prev0 = prev1;
            prev1 = ans;
        }

        return ans;
    }
```

或者用斐波那契数列的通项公式。

```java
public int fib(int N) {
        double goldenRatio = (1 + Math.sqrt(5)) / 2;
        return (int)Math.round(Math.pow(goldenRatio, N)/ Math.sqrt(5));
    }
```
