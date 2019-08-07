# 204. Count Primes

## 题目要求

给定一正整数n，求出小于n的素数个数。

## 怎么写的

先把最笨的办法撸上去，果然运行时间爆炸。

```java
    public boolean isPrime(int n){
        if(n <= 1 || (n > 2 && n % 2 == 0)) return false;
        if(n == 2) return true;
        for (int d =3 ; d*d<=n; d+=2)
            if (n % d == 0) return false;
        return true;
    }

    public int countPrimes(int n) {
        int count = 0;
        for(int i = 2; i < n; i++){
            if(isPrime(i))
                count++;
        }
        return count;
    }
```

如果使用了Sieve of Eratosthenes（质数筛选法）

```java
  public int countPrimes(int n) {
        //Sieve
        if (n <= 2) return 0;
        if (n == 3) return 1;
        boolean[] sieve = new boolean[n];
        sieve[2] = true;
        for (int i = 3; i < n; i+=2)
            sieve[i] = true;
        for (int j = 3; j*j <=n; j+=2){
            if (sieve[j]) {
                for (int k = j+j; k<n; k+=j)
                    sieve[k] = false;
            }
        }
        int count = 1;
        for (int i = 3; i < n; i+=2)
            count += (sieve[i]) ? 1:0;
        return count;
  }
```
