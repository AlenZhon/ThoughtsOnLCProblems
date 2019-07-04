# 9 Palindrome Number

## 题目描述

给定一个integer， 判断它是否是回文数。

>Example 1:  
>**Input**: 121  
>**Output**: true  

>Example 2:
>**Input**: -121  
>**Output**: false  
>**Explanation**: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.  

>Example 3:  
>**Input**: 10  
>**Output**: false  
>**Explanation**: Reads 01 from right to left. Therefore it is not a palindrome.

Follow up:  
Could you solve it without converting the integer to a string?

## 怎么解的

- 如果没有Follow up的限制条件就直接转换成字符串
- 有的话就
  1. 分析边界条件 按照题目意思所有负数都直接返回false
  2. 无脑while 循环把每一个个位分解然后重组成revertedNumber 最后和原来的x比较一下

Submit就直接过了，不过看Solution发现自己还是少考虑数据溢出的情况和循环次数的优化。

## Tricks & Notes

可以只把while循环条件设置到`(x>revertedNumber)`,也就是只重组后半段做比较。  
比较时有奇偶回文数两种情况`return x==revertedNumber || x == revertedNumber /10;`
