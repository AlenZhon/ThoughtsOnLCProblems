# 521. Longest Uncommon Subsequence I

## 题目

两个字符串，找出它们最长的不相同subsequence.

>Given a group of two strings, you need to find the longest uncommon subsequence of this group of two strings. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be any subsequence of the other strings.
>
>A **subsequence** is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.
>
>The input will be two strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.
>
>**Example 1:**
>
>>Input: "aba", "cdc"  
>>Output: 3  
>>Explanation: The longest uncommon subsequence is "aba" (or "cdc"),
because "aba" is a subsequence of "aba",
but not a subsequence of any other strings in the group of two strings.
>
>**Note:**
>
> - Both strings' lengths will not exceed 100.
> - Only letters from a ~ z will appear in input strings.

## 解法

？看不懂题？

看了solution感觉自己像个zz。分析的思路：

1. 如果两个字符串相同，那么没有最长的不相同subsequence。返回-1。
2. 如果两个字符串不同但长度相等，那么它们本身就是最长的不相同subsequence。返回他们的长度。
3. 如果两个字符串长度不相等，那么较长的字符串肯定是是短字符串的不相同subsequence。返回较长的长度。

```java
public int findLUSlength(String a, String b) {
        if (a.equals(b))
            return -1;
        return Math.max(a.length(), b.length());
    }
```
