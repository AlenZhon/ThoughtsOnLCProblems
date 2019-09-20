# 415. Add Strings

## 题目

给出两个字符串表示的大数字，以字符串形式返回两数之和。

>Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.
>
>**Note:**
>
> - The length of both num1 and num2 is < 5100.
> - Both num1 and num2 contains only digits 0-9.
> - Both num1 and num2 does not contain any leading zero.
> - You must not use any built-in BigInteger library or convert the inputs to integer directly.

## 解法

高精度加法。

用StringBuilder存放每位相加的结果。

```java
public String addStrings(String num1, String num2) {
        char[] c1 = num1.toCharArray(), c2 = num2.toCharArray();
        int add = 0, i = c1.length -1, j = c2.length -1;
        StringBuilder ret = new StringBuilder();
        while (i >=0 || j>=0 || add !=0){
            if (i>=0) add += c1[i--] - '0';
            if (j>=0) add += c2[j--] - '0';
            ret.append(add % 10);
            add = (add) / 10;
        }
        return ret.reverse().toString();
    }
```
