# 8. String to Integer (atoi)

## 题目

实现将字符串转换为数字的`atoi`函数。

当字符串开头有若干空格时忽略空格，第一个非空格字符可以是`'+', '-'`表示正负号，如果没有时默认为正。将符号位之后的数字字符转换为数字返回。

如果数字字符后接的其他字符则截断。如果非空格字符后接的不是符号字符或数字字符，或是字符串为空，又或者是字符串全由空格组成，认为这个字符串无法有效转换为数字。

如果无法转换为数字，则返回0，否则返回转换后的数字。

假设我们工作在32位有符号数的范围内。如果数字大于2^31 -1 则返回2^31 - 1，如果数字小于-2^31则返回-2^31。

>Implement `atoi` which converts a string to an integer.
>
>The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
>
>The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
>
>If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
>
>If no valid conversion could be performed, a zero value is returned.
>
>**Note:**
>
> - Only the space character ' ' is considered as whitespace character.
> - Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: `[−2^31,  2^31 − 1]`. If the numerical value is out of the range of representable values, `INT_MAX` (2^31 − 1) or `INT_MIN` (−2^31) is returned.
>
>**Example 1:**
>
>>Input: "42"  
>>Output: 42
>
>**Example 2:**
>
>>Input: "   -42"  
>>Output: -42  
>>Explanation: The first non-whitespace character is '-', which is the minus sign.  
Then take as many numerical digits as possible, which gets 42.
>
>**Example 3:**
>
>>Input: "4193 with words"  
>>Output: 4193  
>>Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
>
>**Example 4:**
>
>>Input: "words and 987"  
>>Output: 0  
>>Explanation: The first non-whitespace character is 'w', which is not a numerical digit or a +/- sign. Therefore no valid conversion could be performed.
>
>**Example 5:**
>
>>Input: "-91283472332"  
>>Output: -2147483648  
>>Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.  
Thefore INT_MIN (−231) is returned.

## 解法

直接写。由于工作在32位环境 (?)所以先判断前30位，再比较最后一位看是否溢出。

```java
public int myAtoi(String str) {
        int i = 0, sign = 1, res = 0,
            INT_MAX = Integer.MAX_VALUE, INT_MIN = Integer.MIN_VALUE;
        if (str.length() == 0) return 0;
        while (i < str.length() && str.charAt(i) == ' ') i++;
        if (i == str.length() || Character.isLetter(str.charAt(i))) return 0;

        if (str.charAt(i) == '-' || str.charAt(i) == '+') {
            sign = str.charAt(i) == '-' ? -1 : 1;
            i++;
        }

        while (i < str.length() && Character.isDigit(str.charAt(i))){
            if (res > INT_MAX / 10 || (res == INT_MAX / 10 && str.charAt(i) > '7'))
                return (sign == 1)? INT_MAX : INT_MIN;
            res = 10 * res + (str.charAt(i++) - '0');
        }
        return res * sign;
    }
```

时间复杂度O(n)，空间O(1)。(2ms)

好奇1ms的解法里用的是什么方法，结果它竟然用`double`类型定义`res`变量，从而绕过了小心翼翼的边界判断？？？  
骚气。
