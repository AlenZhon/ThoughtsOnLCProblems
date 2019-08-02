# 190. Reverse Bits

## 题目描述

给定一32位unsigned int，求出它按位翻转后的值。

>Reverse bits of a given 32 bits unsigned integer.
>
>>**Example 1:**
>>
>>Input: **00000010100101000001111010011100**  
>>Output: **00111001011110000010100101000000**  
>>Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.
>>
>>**Example 2:**
>>
>>Input: **11111111111111111111111111111101**
>>Output: **10111111111111111111111111111111**
>>Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10101111110010110010011101101001.
>
>Note:
>
> - Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
> - In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above the input represents the signed integer `-3` and the output represents the signed integer `-1073741825`.

## 怎么写的

```java
public int reverseBits(int n) {
        int ans = 0, count = 0;
        while (count < 32) {
            ans = (ans << 1) | (n & 0x1);
            n =n >> 1;
            count ++;
        }
        return ans;
    }
```

java中有三种移位运算符，`<<`左移位运算符，低位补0，相当于乘以2的k次方（没有溢出的情况下）；`>>`带符号的右移运算符，高位补符号位；`>>>`不带符号的右移运算符，高位补0。

评论区老哥说的好： 希望在真实场景下大家都是这么写java的：

```java
return Integer.reverse(n);
