# 1071. Greatest Common Divisor of Strings

## 题目

两个字符串S, T，如果说S能够由若干个T拼接而成，那么将其表示为S能被T"整除"。现在给定两个字符串str1, str2,找到这两个字符串的最大公约串X，使得两者都被X整除的同时X的长度最大。

>For strings S and T, we say "T divides S" if and only if S = T + ... + T  (T concatenated with itself 1 or more times)
>
>Return the largest string X such that X divides str1 and X divides str2.
>
>**Example 1:**
>
>>Input: str1 = "ABCABC", str2 = "ABC"  
>>Output: "ABC"
>
>**Example 2:**
>
>>Input: str1 = "ABABAB", str2 = "ABAB"  
>>Output: "AB"  
>
>**Example 3:**
>
>>Input: str1 = "LEET", str2 = "CODE"  
>>Output: ""
>
>**Note:**
>
> - 1 <= str1.length <= 1000
> - 1 <= str2.length <= 1000
> - str1[i] and str2[i] are English uppercase letters.

## 解法

暴力破解。从比较短的字符串入手，比较另一个字符串能否被substring(0, i)整除。同时i还要是两个字符串长度的公约数。

```java
public String gcdOfStrings(String str1, String str2) {
        if (str2.length() == 0 || str1.length() == 0) return "";
        if (str2.length() > str1.length())
            return gcdOfStrings(str2, str1); // str1.length() > str2.length()
        for (int i = str2.length(); i > 0; i--){
            boolean flag = true;
            String div = str2.substring(0, i);
            if (str1.length() % i != 0 || str2.length() % i != 0) continue; //not divide
            for (int j = 0; j < str1.length() / i; j++) {
                if (!str1.substring(j * i , (j + 1) * i).equals(div)){
                    flag = false;
                    break;
                }
            }
            if (flag) return div;
        }
        return "";
    }
```

提交上去1ms。0ms的解法用的递归的思路，类似于求最大公约数的辗转相除法。

```java
public String gcdOfStrings(String str1, String str2) {
        if (str2.length() > str1.length())
            return gcdOfStrings(str2, str1); // str1.length() > str2.length()
        else if (!str1.startWith(str2))
            return "";
        else if (str2.isEmpty())
            return str1;
        else
            return gcdOfStrings(str1.substring(str2.length()), str2);
    }
```
