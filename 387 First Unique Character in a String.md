# 387. First Unique Character in a String

## 题目

>Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.
>
>**Examples:**
>
>>s = "leetcode"  
>>return 0.
>>
>>s = "loveleetcode",  
>>return 2.
>
>**Note:** You may assume the string contain only lowercase letters.

给定一字符串（可假设只含小写字母），找到第一个不重复字符的下标。若该字符不存在则返回-1。

## 解法

都是套路。遍历两次时间复杂度O(N)，空间复杂度O(1)。如果用`HashMap`的话空间复杂度就得O(N)。

```java
    char[] c = s.toCharArray();
        int[] count = new int[26];
        for (char ch : c)
            count[ch-'a']++;
        for (int i =0; i<c.length; i++)
            if (count[c[i] -'a'] == 1) return i;
        return -1;
    }
```
