# 279. Perfect Squares

## 题目

给定一正整数n，将其表示成若干个平方数之和。计算和式中使用最少平方数的个数。

>Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.
>
>**Example 1:**
>
>>Input: n = 12  
>>Output: 3  
>>Explanation: 12 = 4 + 4 + 4.  
>
>Example 2:
>
>>Input: n = 13  
>>Output: 2  
>>Explanation: 13 = 4 + 9.

## 解法

想了想，每个正整数肯定都可以写出和式。写写前面几个找找规律。

> `count[0] = 0`  
> `count[1] = 1 = count[0] + 1`  
> `count[2] = 2 = count[1] + 1`  
> `count[3] = 3 = count[2] + 1`  
> `count[4] = 1 = min(count[4-1*1] +1, count[4-2*2] +1)`  
> ...
> `count[13] = 2 = min(count[13-1*1] +1, count[13-2*2] +1, count[13-3*3] +1)`  
> ...  
> `count[n] = min(count[n-1*1]+1, ...,count[n-i*i]+1) when i < n/i`  

一个动态规划问题。

```java
class Solution {
    public int numSquares(int n) {
        int[] count = new int[n+1];
        count[0] = 0;
        for (int i = 1; i<=n; i++) {
            int min = Integer.MAX_VALUE, j = 1;
            while (i- j*j >=0) {
                min = Math.min(min, count[i- j*j]+1);
                j++;
            }
            count[i] = min;
        }
        return count[n];
    }
}
```

时间复杂度O(n*sqrt(n))， 空间复杂度O(n)。  
内层循环变量 `j` 可以从 `Math.sqrt(i)` 开始递减，减少一些循环次数。同时可以对 `i` 是完全平方数的情况提前判断。

## 另一种解法（基于[拉格朗日四平方和定理](https://en.wikipedia.org/wiki/Lagrange%27s_four-square_theorem)）

>四平方和定理：任何一个正整数都可以表示成不超过四个整数的平方之和。

根据这个定理，程序的输出结果只有`1,2,3,4`四种情况。

1. 如果n就是平方数，返回1。
2. 如果n可以写成4^n(8m+7)的形式，返回4.（由[勒让德三平方和定理](https://en.wikipedia.org/wiki/Legendre%27s_three-square_theorem#History)证明）
3. 遍历i从1到sqrt(n)，如果n-i是平方数，表示可写成两个数的平方和，返回2.
4. 返回3.

```java
class Solution {
    private boolean isSquare(int n) {
        int i = (int) Math.sqrt(n);
        return (i*i == n);
    }
    public int numSquares(int n) {
        if (n<=0) return 0;

        if (isSquare(n)) return 1;

        int m = n;
        while (m %4 ==0) {m = m>> 2;}
        if (m % 8 == 7) return 4;

        for (int i = 1; i<= Math.sqrt(n); i++) {
            int remain = n - i*i;
            if (isSquare(remain)) return 2;
        }
        return 3;
    }
}
```

时间空间复杂度骤降到O(sqrt(n))和O(1)，数学真是推动人类进步。
