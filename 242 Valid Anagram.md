# 242. Valid Anagram

## 题目

>Given two strings s and t , write a function to determine if t is an anagram of s.
>
>**Example 1:**
>
>>Input: s = "anagram", t = "nagaram"  
>>Output: true  
>
>**Example 2:**
>
>>Input: s = "rat", t = "car"  
>>Output: false
>
>**Note:**
>You may assume the string contains only lowercase alphabets.
>
>**Follow up:**
>What if the inputs contain unicode characters? How would you adapt your solution to such case?

## 解法

> anagram : a word, phrase, or name formed by rearranging the letters of another, such as cinema , formed from iceman.  

看懂了anagram的意思之后发现一个记录字母频次的水题。主要的就是从字符到ASCII数组（题目限定是小写字母就`new int[26]`）的映射。

一开始我写了两个映射的数组，最后比较。写完发现完全可以写成一个，最后看数组里哪个字母频次不为0。

时间复杂度和两个字符串长度之和有关。把string对象的charAt()方法改成toCharArray()可以在平台上减少2ms的运行时间。

```java
 public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] dict = new int[26];
        for (char c : s.toCharArray())
            dict[c - 'a'] +=1;
        for (char c : t.toCharArray())
            dict[c - 'a'] -=1;
        for (int i =0; i < 26; i++)
            if (dict[i] != 0) return false;
        return true;
    }
```

也有人直接两个toCharArray()+两个Arrays.sort()，最后equals()比较。
