# 459. Repeated Substring Pattern

## 题目

给定一个非空字符串s，判断s是否能由其中的字串重复若干次得到。

>Given a **non-empty** string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.
>
>**Example 1:**
>
>>Input: "abab"  
>>Output: True  
>>Explanation: It's the substring "ab" twice.
>
>**Example 2:**
>
>>Input: "aba"  
>>Output: False  
>
>**Example 3:**  
>
>>Input: "abcabcabcabc"  
>>Output: True  
>>Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)

## 解法

一开始的想法： 先确定子串，再判断是否能构成原字符串。如何确定子串？想的是检测第一个字符再次出现时的位置。

撸了一个代码提交上去，首先发现自己对substring(int startIndex, int endIndex)方法的理解有误，该方法返回的是[startIndex, endIndex)范围的字符串。左闭右开而不是闭区间。

改了之后发现自己没有考虑到子串中也会有重复出现的字符。例如原始字符串`"abaababaab"`，可看做由`"abaab"`重复一次得到。

转变思路，从子串长度入手。如果存在满足条件的子串，则子串的长度必定是原始长度的因子。

```java
public boolean repeatedSubstringPattern(String s) {
    int len = s.length();
    for(int i=len/2 ; i>=1 ; i--) {
        if (len % i != 0) continue;
        int m = len/i, j = 1;
        String subS = s.substring(0,i);
        for(; j < m; j++)
          if(!subS.equals(s.substring(j*i,i+j*i))) break;
        if(j==m) return true;
    }
    return false;
}
```
