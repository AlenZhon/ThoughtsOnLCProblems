# 476. Number Complement

## 题目

给定一个Integer正整数，返回它有效位数内比特翻转后的对应数。如`5(101) -> 2(10)`。

>Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.
>
>**Note:**
>
> - The given integer is guaranteed to fit within the range of a 32-bit signed integer.
> - You could assume no leading zero bit in the integer’s binary representation.
>
>**Example 1:**
>
>>Input: 5  
>>Output: 2  
>>Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
>
>**Example 2:**
>
>>Input: 1  
>>Output: 0  
>>Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.

## 解法

同或运算？首先取反，然后把高位的那些1全部置0。但问题是怎么判断高位的那些1有多少位？

换个角度想。`5 + 2 = 7 (111)` `1 + 0 = 1 (1)` 只需找到比num大的全1数，然后相减即可。

```java
public int findComplement(int num) {
        int i = 1;
        while (i< num) {i = (i<< 1) +1;}
        return i - num;
    }
```

关于前面那个思路，讨论区里有位大佬使用了built-in函数去确定最高位的1出现在哪里。

```java
 public int findComplement(int num) {
        return ~num & (Integer.highestOneBit(num) - 1);
    }
```
