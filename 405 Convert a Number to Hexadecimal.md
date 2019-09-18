# 405. Convert a Number to Hexadecimal

## 题目

将一个整数转换为16进制。具体输出格式要求见下。

>Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, two’s complement method is used.
>
>**Note:**
>
> - All letters in hexadecimal (a-f) must be in lowercase.
> - The hexadecimal string must not contain extra leading 0s. If the number is zero, it is represented by a single zero character '0'; otherwise, the first character in the hexadecimal string will not be the zero character.
> - The given number is guaranteed to fit within the range of a 32-bit signed integer.
> - You must not use any method provided by the library which converts/formats the number to hex directly.
>
>**Example 1:**
>
>>Input: 26  
>>Output: "1a"
>
>**Example 2:**
>>Input: -1  
>>Output: "ffffffff"

## 解法

Straight forward. 无符号右移四位，对应哪个16进制位就在字符串前部添加。

```java
public String toHex(int num) {
        char[] hex = {'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'};
        if (num == 0) return "0";
        String res = new String();
        while (num != 0) {
            res = hex[num & 15] + res;
            num = num >>> 4;
        }
        return res;
    }
```

不用StringBuffer啥的也能在 OJ 运行时间0ms。估计是给的32位有符号整数范围太小，最多也就字符串拼接8次，运行时间相差不大。
