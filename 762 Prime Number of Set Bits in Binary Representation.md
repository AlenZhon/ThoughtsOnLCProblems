# 762. Prime Number of Set Bits in Binary Representation

## 题目

给定一个正整数的上下界 `[L, R]`，将区间中的每一个整数写成二进制形式之后，记录下二进制形式中1出现次数为质数的整数个数。

数值范围`1<=L <=R <= 1e6`。

>Given two integers L and R, find the count of numbers in the range `[L, R]` (inclusive) having a prime number of set bits in their binary representation.
>
>(Recall that the number of set bits an integer has is the number of 1s present when written in binary. For example, 21 written in binary is 10101 which has 3 set bits. Also, 1 is not a prime.)
>
>**Example 1:**
>
>>Input: L = 6, R = 10  
>>Output: 4  
>>Explanation:  
>>6 -> 110 (2 set bits, 2 is prime)  
>>7 -> 111 (3 set bits, 3 is prime)  
>>9 -> 1001 (2 set bits , 2 is prime)  
>>10->1010 (2 set bits , 2 is prime)  
>
>**Example 2:**
>
>>Input: L = 10, R = 15  
>>Output: 5  
>>Explanation:  
>>10 -> 1010 (2 set bits, 2 is prime)  
>>11 -> 1011 (3 set bits, 3 is prime)  
>>12 -> 1100 (2 set bits, 2 is prime)  
>>13 -> 1101 (3 set bits, 3 is prime)  
>>14 -> 1110 (3 set bits, 3 is prime)  
>>15 -> 1111 (4 set bits, 4 is not prime)  
>
>**Note:**
>
> - L, R will be integers L <= R in the range `[1, 10^6]`.
> - R - L will be at most 10000.

## 解法

由于给定了数值范围，10^6有20个bit，所以只需要判断1 bit的个数是否在`(2,3,5,7,11,13,17,19)`的质数集合中。

```java
public int countPrimeSetBits(int L, int R) {
        int count = 0;
        for (int i = L; i<= R; i++){
            int ones = countSetBits(i);
            if (isPrime(ones)) count++;
        }
        return count;
    }
    private int countSetBits(int num){
        int x = num, ret = 0;
        while (x > 0) {
            ret += x & 1;
            x >>= 1;
        }
        return ret;
    }
    private boolean isPrime(int x){
        return (x == 2 || x ==3 || x == 5|| x == 7 || x == 11 || x == 13 || x == 17 || x == 19);
    }
```

其中，  

- `countSetBits()`方法可以直接用API `Integer.bitCount()`代替。  
- `isPrime()`方法可以用hash数组int[20]代替。在指定位置置1.

```java
public int countPrimeSetBits(int L, int R) {
        int count = 0;
        int[] h = new int[20];
        h[2] = 1; h[3] = 1; h[5] = 1; h[7] = 1; h[11] = 1; h[13]= 1; h[17]= 1; h[19] =1;
        for (int i = L; i<= R; i++){
            int ones = Integer.bitCount(i); //countSetBits(i);
            count+= h[ones];
            //if (isPrime(ones)) count++;
        }
        return count;
    }
```
