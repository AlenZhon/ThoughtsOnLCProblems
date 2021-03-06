# 507. Perfect Number

## 题目

判断一个整数是不是完美数。完美数的定义： 除了该数本身，其他因数之和等于该数。

>We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.  
>Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.
>
>**Example:**
>
>>Input: 28  
>>Output: True  
>>Explanation: 28 = 1 + 2 + 4 + 7 + 14
>
>**Note:** The input number n will not exceed 100,000,000. (1e8)

## 解法

由于是所有因数，所以只需从2遍历到`Math.sqrt(n)`即可找到所有的因数对。（先判断1，然后先从result里减1。）

```java
public boolean checkPerfectNumber(int num) {
        if (num <= 1) return false;
        int result = num - 1;
        for (int i = 2; i<= Math.sqrt(num); i++) {
            if (num % i == 0) {
                result-= i;
                result-= num/i;
            }
            if (result < 0) break;
        }
        return result == 0 ? true : false;
    }
```

时间复杂度O(Math.sqrt(n))，空间复杂度O(1)

### Eucild-Euler Theorem

>Euclid proved that `2^{p−1}(2^p − 1)` is an even perfect number whenever `2^{p−1}(2^p − 1)` is prime, where `p` is prime.
>
>For example, the first four perfect numbers are generated by the formula `2^{p−1}(2^p − 1)`, with p a prime number, as follows:
>
>>for p = 2:   2^1(2^2 − 1) = 6  
>>for p = 3:   2^2(2^3 − 1) = 28  
>>for p = 5:   2^4(2^5 − 1) = 496  
>>for p = 7:   2^6(2^7 − 1) = 8128.  
>
>Prime numbers of the form `2^p - 1` are known as Mersenne primes. For `2^p - 1` to be prime, it is necessary that `p` itself be prime. However, not all numbers of the form `2^p - 1` with a prime `p` are prime; for example, `2^11−1 = 2047 = 23×89` is not a prime number.
>
>You can see that for small value of `p`, its related perfect number goes very high. So, we need to evaluate perfect numbers for some primes `(2,3,5,7,13,17,19,31)` only, as for bigger prime its perfect number will not fit in 64 bits.

```java
public int pn(int p) {
        return (1 << (p - 1)) * ((1 << p) - 1);
    }
    public boolean checkPerfectNumber(int num) {
        int[] primes=new int[]{2,3,5,7,13,17,19,31};
        for (int prime: primes)
            if (pn(prime) == num)
                return true;
        return false;
    }
```
