# 263. Ugly Number

## 题目

判断给定整数是否是丑数。除了第一个丑数1，其他丑数的定义是只含有质因子2，3，5的数。

>Write a program to check whether a given number is an ugly number.
>
>Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.
>
>**Example 1:**
>
>>Input: 6  
>>Output: true  
>>Explanation: 6 = 2 × 3
>
>**Example 2:**
>
>>Input: 8  
>>Output: true  
>>Explanation: 8 = 2 × 2 × 2
>
>**Example 3:**
>
>>Input: 14
>>Output: false
>>Explanation: 14 is not ugly since it includes another prime factor 7.
>
>**Note:**
>
>- 1 is typically treated as an ugly number.
>- Input is within the 32-bit signed integer range: `[−2^31,  2^31 − 1]`.

## 解法

既然是ugly number，先用一下ugly的暴力整除办法。既然数值范围给定，那么总共整除的最大次数也就可以确定。

```java
 public boolean isUgly(int num) {
        if (num < 1) return false;
        if (num < 7) return true;
        while (num % 5 == 0) {num/=5;}
        while (num % 3 == 0) {num/=3;}
        while (num % 2 == 0) {num/=2;}
        return (num == 1);
    }
```

运行时间1ms。

也可以写成这样。被4整除的话减少一次循环次数2333.

```java
for (int i=2; i<6 && num>0; i++)
    while (num % i == 0)
        num /= i;
return num == 1;
```
