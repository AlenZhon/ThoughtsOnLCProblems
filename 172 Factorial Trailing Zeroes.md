# 172. Factorial Trailing Zeroes

## 题目描述

给定一个正整数n，求出n的阶乘的结尾有多少个0.

>Given an integer n, return the number of trailing zeroes in n!.
>
>Example 1:
>
>Input: 3
>Output: 0
>Explanation: 3! = 6, no trailing zero.
>
>Example 2:
>
>Input: 5
>Output: 1
>Explanation: 5! = 120, one trailing zero.
>
>Note: Your solution should be in logarithmic time complexity.

## 怎么解的

要求结尾有多少个0，也就是需要看阶乘式子n!里有多少个质因子2和多少个质因子5。

也就是`n! = 2^x * 5^y * ...`  
其中当n大于5时，x>=y，所以只需要记下5的个数y。而y又可以通过计算n能被5整除的次数得来。

> O(log_5(N)) (base 5!) is faster than any polynomial. You need no more than 14 iterations to get the result. You just need to count how many times 5 appears in n! during multiplication in different forms: 5, 25, 125, 625, ... . when any 5 is multiplied by 2 (we have many of them) then we get 0 at the end.

```java
public int trailingZeroes(int n) {
        int fivecount =0;
        while (n > 0) {
            n /=5;
            fivecount += n;
        }
        return fivecount;
    }
```

如果用递归的思想：

```java
public int trailingZeroes(int n) {
        if (n<5) return 0;
        return n/5 + trailingZeroes(n/5);
}
```
