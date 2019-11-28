# 1009. Complement of Base 10 Integer

## 题目

对于任意一个非负整数，找到它二进制表示形式按位取反后的值。如`5 = (101)_2` 按位取反后为`(010)_2 = 2`

>Every non-negative integer N has a binary representation.  For example, 5 can be represented as "101" in binary, 11 as "1011" in binary, and so on.  Note that except for N = 0, there are no leading zeroes in any binary representation.
>
>The complement of a binary representation is the number in binary you get when changing every 1 to a 0 and 0 to a 1.  For example, the complement of "101" in binary is "010" in binary.
>
>For a given number N in base-10, return the complement of it's binary representation as a base-10 integer.
>
>
>
>**Example 1:**
>
>>Input: 5  
>>Output: 2  
>>Explanation: 5 is "101" in binary, with complement "010" in binary, which is 2 in base-10.
>
>**Example 2:**
>
>>Input: 7  
>>Output: 0  
>>Explanation: 7 is "111" in binary, with complement "000" in binary, which is 0 in base-10.
>
>**Example 3:**
>
>>Input: 10  
>>Output: 5  
>>Explanation: 10 is "1010" in binary, with complement "0101" in binary, which is 5 in base-10.
>
>**Note:**
>
> - 0 <= N < 10^9

## 解法

根据题意， N不会超过 2^30 = 1,073,741,824。
考虑到按位取反之后的数b和原数a相加，有

`a + b = (11...1)_2 = 2 ^ Math.ceil(log2(a)) - 1`

比如a = 12 那么Math.ceil(log2(a)) = 4，所以 b = 2 ^ 4 - 1 - a = 15 - 12 = 3.

如果不用log的话就迭代往上乘。

```java
public int bitwiseComplement(int N) {
        int a = 1;
        if (N == 0) return 1;
        for (int i = 1; i < 31; i++){
            if (a <= N && N < a * 2) return a*2 - 1 - N;
            a *=2;
        }
        return 0;
    }
```
