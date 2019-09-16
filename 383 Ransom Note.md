# 383. Ransom Note

## 题目

>Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.
>
>Each letter in the magazine string can only be used once in your ransom note.
>
>**Note:**
>You may assume that both strings contain only lowercase letters.
>
>>canConstruct("a", "b") -> false  
>>canConstruct("aa", "ab") -> false  
>>canConstruct("aa", "aab") -> true

说实话一开始没太看懂题目。查了下`ransom note`名为勒索信，关于它经常有个梗说勒索信上的字母为了防止笔迹泄露都是用杂志上的词语拼贴的。

所以这题的意思是给定杂志字符串和勒索信字符串，判断能否由杂志拼贴出勒索信。杂志字符串的每个字母只能使用一次（比如杂志为`aab`，勒索信最多只能出现两个`a`）。

## 解法

正常的肯定用HashMap存`<char key, int count>`了。不过这里既然给定了全是小写字母，那不如直接构造`int[26]`存字母出现的次数。

```java
public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() == 0)return true;
        int[] dict = new int[26];
        for (char ch : magazine.toCharArray())
            dict[ch -'a']++;
        for (char ch : ransomNote.toCharArray())
            if (--dict[ch - 'a'] < 0) return false;
        return true;
    }
```

把String的`charAt()`改成`toCharArray()`在 LeetCode OJ 的运行时间上减少了2ms。
