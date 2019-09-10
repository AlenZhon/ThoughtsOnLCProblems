# 344. Reverse String

## 题目

给定一个字符数组，其中每个元素都是可打印的ASCII码字符。要求空间复杂度O(1)的情况下完成数组的 in-place 转置。

>Write a function that reverses a string. The input string is given as an array of characters char[].
>
>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
>
>You may assume all the characters consist of printable ascii characters.
>
>**Example 1:**
>
>>Input: ["h","e","l","l","o"]  
>>Output: ["o","l","l","e","h"]
>
>**Example 2:**
>>
>>Input: ["H","a","n","n","a","h"]  
>>Output: ["h","a","n","n","a","H"]  

## 解法

水题。char temp + 头尾指针。

由于输入参数是`char[] s`使得值得讨论的点减少了一大半。
