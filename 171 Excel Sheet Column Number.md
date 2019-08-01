# 171. Excel Sheet Column Number

## 题目描述

给定一个excel表的列数，把它转化成数字。（# 168的逆运算）  

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...

>Given a column title as appear in an Excel sheet, return its corresponding column number.
>
>Example 1:
>
>Input: "A"  
>Output: 1
>
>Example 2:
>
>Input: "AB"  
>Output: 28
>
>Example 3:
>
>Input: "ZY"  
>Output: 701

## 怎么解的

转成字符数组，秒了。

```java
public int titleToNumber(String s) {
    int ans =0;
    char[] c = s.toCharArray();
    for (int i = 0; i < c.length; i++) {
        ans = ans *26 + ((int)c[i] - 64);
    }
    return ans;
}
```
