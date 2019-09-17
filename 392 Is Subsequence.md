# 392. Is Subsequence

## 题目

给定字符串s和t， 判断s是不是t的子串。子串在这里定义为可由源字符串删去任意字母（也可不删去），保留原本顺序得到的新字符串。可假设t是一个非常长的字符串而s是个短串，两者均由小写英文字母组成。

如果有许多个s（个数大于1B），应该如何修改代码依次判断它们是否是t的子串？

>Given a string s and a string t, check if s is subsequence of t.
>
>You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).
>
>A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).
>
>**Example 1:**
>>s = "abc", t = "ahbgdc"  
>>Return true.
>
>**Example 2:**
>>s = "axc", t = "ahbgdc"  
>>Return false.
>
>**Follow up:**
>If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?
>
>**Credits:**
Special thanks to `@pbrother` for adding this problem and creating all test cases.

## 解法

直接暴力遍历，时间复杂度O(N)，N为t字符串中的字符个数。注意边界条件，空串也算是子串。

```java
public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) return true;
        char[] s1 = s.toCharArray();
        char[] t1= t.toCharArray();
        int ps = 0, pt =0;
        while (pt < t1.length) {
            if (s1[ps] == t1[pt]) {
                ps++;
                if (ps == s1.length) return true;
            }
            pt++;
        }
        return false;
    }
```

`indexOf(String str, int fromIndex)`提供了类似的功能。返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引fromIndex开始，如果不存在则返回-1。则代码改写为：

```java
 public boolean isSubsequence(String s, String t) {
        for (int i = 0, j = 0; i < s.length(); i++) {
            int temp = t.indexOf(s.charAt(i), j);
            if (temp == -1) return false;
            j = temp+1;
        }
        return true;
    }
```

关于follow-up的问题，可以将t的每个字符出现的下标预先存储（考虑到字符个数很多而英文字符只有26个），再对每个s进行检查看其中每个字符是否按顺序出现在位置上。
