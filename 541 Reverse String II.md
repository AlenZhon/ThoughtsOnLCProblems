# 541. Reverse String II

## 题目

给定一个字符串和一个正整数k。  
对字符串的每2k个字符，将前k个字符reverse而后k个字符保留原始顺序。当字符串结尾字符小于k个时，将这些字符reverse；否则，将结尾字符的前k个reverse而后面小于k个字符保留原始顺序。

>Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.
>
>**Example:**
>
>>Input: s = "abcdefg", k = 2  
>>Output: "bacdfeg"
>
>**Restrictions:**
>
> - The string consists of lower English letters only.
> - Length of the given string and k will in the range [1, 10000]

## 解法

直接翻译题目。每k个字符判断一下oddK是否为真。为真则reverse，不为真则什么都不做。

```java
public String reverseStr(String s, int k) {
        if (k <1) return s;
        char[] c = s.toCharArray();
        boolean oddK = true;
        for (int index = 0; index < c.length; index+=k)
            if (oddK) {
                int head = index, tail = Math.min(index + k - 1, c.length - 1);
                while (head < tail) {
                    char temp = c[head];
                    c[head++] = c[tail];
                    c[tail--] = temp;
                }
                oddK = false;
            } else {
                oddK = true;
            }
        return String.valueOf(c);
    }
```

时间复杂度和空间复杂度都为O(N)，与字符串长度相关。
发现oddK的判断完全可以省略，直接每2k个字符判断一下就行。

```java
public String reverseStr(String s, int k) {
        if (k <1) return s;
        char[] c = s.toCharArray();
        for (int index = 0; index < c.length; index+=2* k) {
                int head = index, tail = Math.min(index + k - 1, c.length - 1);
                while (head < tail) {
                    char temp = c[head];
                    c[head++] = c[tail];
                    c[tail--] = temp;
                }
        }
        return new String(c);
    }
```
