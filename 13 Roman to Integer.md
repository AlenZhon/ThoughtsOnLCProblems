# 13 Roman to Integer

## 题目描述

将一个数值范围在1-3999的罗马数字转换成整数。

>Symbol   |    Value  
>:-:|:-:  
>I   |          1  
>V    |         5  
>X    |         10
>L     |        50
>C     |        100
>D     |        500
>M     |        1000

>There are six instances where subtraction is used:  
    >- I can be placed before V (5) and X (10) to make 4 and 9.
    >- X can be placed before L (50) and C (100) to make 40 and 90.  
    >- C can be placed before D (500) and M (1000) to make 400 and 900.

## 怎么解的

一开始的想法是用遍历String中每一个字符 + `switch case`语句，在除了`case ‘I’`中`if`把多加的减回来。
```java
class Solution {
    public int romanToInt(String s) {
        int i = 0, ans = 0;
        while (i < s.length()) {
            switch (s.charAt(i))
            {
                case 'M':
                    ans += 1000;
                    if (i>0 && s.charAt(i-1)=='C') {ans =ans -2*100;}
                    break;
                case 'D':
                    ans+= 500;
                    if (i>0 && s.charAt(i-1)=='C') {ans =ans -2*100;}
                    break;
                case 'C':
                    ans+= 100;
                    if (i>0 && s.charAt(i-1)=='X') {ans =ans -2*10;}
                    break;
                case 'L':
                    ans+= 50;
                    if (i>0 && s.charAt(i-1)=='X') {ans =ans -2*10;}
                    break;
                case 'X':
                    ans+= 10;
                    if (i>0 && s.charAt(i-1)=='I') {ans =ans -2*1;}
                    break;
                case 'V':
                    ans+= 5;
                    if (i>0 && s.charAt(i-1)=='I') {ans =ans -2*1;}
                    break;
                case 'I':
                    ans += 1;
                    break;
            } i += 1;
        }
      return ans;
    }
}
```

之后又想到可以先把String按照每一位转化成对应的数组`num[]`,遍历它的前n-1个元素。

```java
    if (num[i]< num[i+1]) {
        ans -= num[i];
    } else {
        ans += num[i];
    }
```

加上最后一个元素即可。
