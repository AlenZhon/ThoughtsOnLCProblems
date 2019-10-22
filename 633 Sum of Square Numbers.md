# 633. Sum of Square Numbers

## 题目

给定一个非负整数，判断它能否写成两个数的平方和。

>Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a2 + b2 = c.
>
>**Example 1:**
>
>>Input: 5  
>>Output: True  
>>Explanation: `1 * 1 + 2 * 2 = 5`
>
>**Example 2:**
>
>>Input: 3  
>>Output: False

## 解法

用完全平方数测了一下，发现返回的是true。意味着`4 = 2 *2 + 0 *0`是允许的.

### straight-forward (4ms)

时间复杂度O(sqrt(c) * log_c)，我们遍历了`[0, sqrt(c)]`确定a，而每次对c - a*a开根号，最坏情况下需要O(log_c)的时间。

```java
public boolean judgeSquareSum(int c) {
        int n = (int) Math.sqrt(c);
        if (n* n == c) return true;
        for (int a = n; a> 0; a--) {
            int remain = c - a * a;
            int b = (int) Math.sqrt(remain);
            if (b * b == remain) return true;
        }
        return false;
    }
```

### two-pointers (2ms)

两个指针

```java
public boolean judgeSquareSum(int c) {
        int a = 0, b = (int) Math.sqrt(c);
        while (a <=b) {
            int curr = a * a + b * b;
            if (curr == c) return true;
            if (curr > c) b--;
            if (curr < c) a++;
        }
        return false;
    }
```

### 费马平方和定理 (0ms)

费马定理（[Fermat's theorem](https://wstein.org/edu/124/lectures/lecture21/lecture21/node2.html)）：  
> Any positive number `n` is expressible as a sum of two squares if and only if the prime factorization of `n`, every prime of the form `(4k+3)` occurs an even number of times.  
> 任何正数n能表示为两个数的平方和，当且仅当n的质因子分解中，(4k + 3) 型的质数出现了偶数次。

所以， 我们首先找到c的质因数分解中(4k + 3)的质因子和它出现的次数。如果该质因子出现次数是奇数次就直接返回false。

如果c本身是一个质数，则不会被任意质数整除。于是我们判断它是否是一个(4k + 3)型的质数。如果是，则它本身出现了奇数次，返回false。

```java
public boolean judgeSquareSum(int c) {
        for (int i = 2; i * i <= c; i++) {
            int count = 0;
            if (c % i == 0) {
                while (c % i == 0) {
                    count++;
                    c /= i;
                }
                if (i % 4 == 3 && count % 2 != 0)
                    return false;
            }
        }
        return c % 4 != 3;
    }
```
