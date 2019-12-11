# 1160. Find Words That Can Be Formed by Characters

## 题目

给定一个字符串`chars`和字符串数组`words`，判断words中的每一个字符串是否只由`chars`的字母组成（每个字母仅限用一次）。计算满足条件的字符串长度之和。

>You are given an array of strings `words` and a string `chars`.
>
>A string is good if it can be formed by characters from chars (each character can only be used once).
>
>Return the sum of lengths of all good strings in words.
>
>**Example 1:**
>
>>Input: words = ["cat","bt","hat","tree"], chars = "atach"  
>>Output: 6  
>>Explanation:  
>>The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.
>
>**Example 2:**
>
>>Input: words = ["hello","world","leetcode"], chars = "welldonehoneyr"  
>>Output: 10  
>>Explanation:  
>>The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.
>
>**Note:**
>
> - 1 <= words.length <= 1000
> - 1 <= words[i].length, chars.length <= 100
> - All strings contain lowercase English letters only.

## 解法

计算字符频次的水题。

一开始的写法。 (8ms)

```java
public int countCharacters(String[] words, String chars) {
        int[] ch = new int[26];
        for (char c : chars.toCharArray())
            ch[c - 'a']++;
        int len = 0;
        for (String word : words){
            int[] chtmp = new int[26];
            boolean flag = true;
            for (char c : word.toCharArray())
                chtmp[c - 'a']++;
            for (int i = 0; i< 26; i++)
                if (chtmp[i] > ch[i]) {flag = false; break;}
            if (flag) len += word.length();
        }
        return len;
    }
```

实际上不需要对每个word都统计完字母频次才比较。只要出现了字母频次大于chars字母频次就可以不比了。

修改后的写法 (2ms) 如果不用子函数`flag()`的话是4ms。

```java
public int countCharacters(String[] words, String chars) {
        int[] ch = new int[26];
        for (char c : chars.toCharArray())
            ch[c - 'a']++;
        int len = 0;
        for (String word : words)
            if (flag(word, ch)) len += word.length();
        return len;
    }
    private boolean flag(String word, int[] ch){
        int[] chtmp = new int[26];
        for (char c : word.toCharArray()){
            if (chtmp[c - 'a'] == ch[c - 'a'])
                return false;
            else
                chtmp[c - 'a']++;
        }
        return true;
    }
```
