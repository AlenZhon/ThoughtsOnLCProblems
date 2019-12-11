# 1175. Prime Arrangements

## 题目

给定整数n，范围`[1, 100]`。把[1,n]这n个数中的质数排在质数下标，合数排在合数下标，问总共有几种排列方法？

下标从1开始。排列方法的个数可能很大，程序返回对(10^9 + 7)的取余。

>Return the number of permutations of 1 to n so that prime numbers are at prime indices (1-indexed.)
>
>(Recall that an integer is prime if and only if it is greater than 1, and cannot be written as a product of two positive integers both smaller than it.)
>
>Since the answer may be large, return the answer modulo 10^9 + 7.
>
>**Example 1:**
>
>>Input: n = 5  
>>Output: 12  
>>Explanation: For example [1,2,5,4,3] is a valid permutation, but [5,2,3,4,1] is not because the prime number 5 is at index 1.
>
>**Example 2:**
>
>>Input: n = 100  
>>Output: 682289015  
>
>**Constraints:**
>
> - 1 <= n <= 100

## 解法

稍加分析，即可得出排列方式为（质数个数的阶乘）*（合数个数的阶乘）。

计算质数个数用了筛法。 参考 *#204 Count Primes*

```java
    public int numPrimeArrangements(int n) {
        if (n == 1) return 1;
        boolean[] sieve = new boolean[n + 1];
        sieve[2] = true;
        for (int i = 3; i < sieve.length; i+=2)
            sieve[i] = true;
        for (int j = 3; j * j < sieve.length; j+=2)
            if (sieve[j])
                for (int k = j+ j; k < sieve.length; k+=j)
                    sieve[k] = false;
        int numPrimes = 0;
        long ret = 1;
        for (boolean item : sieve)
            if (item) numPrimes++;
        int MOD = (int)(1e9 + 7);
        for (int i = 2; i <= numPrimes; i++)
            ret = (ret * i) % MOD;
        for (int i = 2; i <= n - numPrimes; i++)
            ret = (ret * i) % MOD;
        return (int)ret;
    }
```

ret一定要定义为long，不然在累乘时会出现OverFlow。

Solution里面的1ms解法：

```java
public int numPrimeArrangements(int n) {
        int[] non = new int[n+1];
        int[] cnt = {0, 1};
        long res = 1;
        for (int i=2; i<=n; i++) {
            if (non[i] == 0)
                for (int m=i*i; m<=n; m+=i)
                    non[m] = 1;
            res = res * ++cnt[non[i]] % 1_000_000_007;
        }
        return (int) res;
    }
```
