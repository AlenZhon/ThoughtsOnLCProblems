# 953. Verifying an Alien Dictionary

## 题目

假设一个外星文明也是用的26个英文字母，但是它们的字母表顺序可能和我们的不同。给定一个String[]， 判断这个字符串数组是否按照它们的字母表先后顺序升序排列。（空字符视作小于所有字符。）

>In an alien language, surprisingly they also use english lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.
>
>Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographicaly in this alien language.
>
>**Example 1:**
>
>>Input: words = `["hello","leetcode"]`, order = `"hlabcdefgijkmnopqrstuvwxyz"`  
>>Output: true  
>>Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
>
>**Example 2:**
>
>>Input: words = `["word","world","row"]`, order = `"worldabcefghijkmnpqstuvxyz"`  
>>Output: false  
>>Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
>
>**Example 3:**
>
>>Input: words = `["apple","app"]`, order = `"abcdefghijklmnopqrstuvwxyz"`  
>>Output: false  
>>Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character (More info).
>
>**Constraints:**
>
> - 1 <= words.length <= 100
> - 1 <= words[i].length <= 20
> - order.length == 26
> - All characters in words[i] and order are English lowercase letters.

## 解法

首先构造一个哈希表，完成英文字母到外星字母顺序的映射。  

然后每次比较相邻的两个字符串s1, s2的第`j`位字符，如果前一个小于后一个，就说明两者按照顺序排列，比较s2,s3；如果前一个大于后一个，说明s1,s2没按顺序排列，`return false`；如果前一个等于后一个，就比较`j+1`位字符。

注意，如果比到字符串结尾还没分出来，就判断是否出现了 ("apple","app") 的情况，此时相当于判断条件`(j == s2.length() && j < s1.length)`是否满足。

```java
public boolean isAlienSorted(String[] words, String order) {
        int[] dict = new int[26];
        for (int i = 0; i< order.length(); i++)
            dict[order.charAt(i) - 'a'] = i;

        for (int i = 1; i< words.length; i++) {
            int j = 0;
            while (j < Math.min(words[i-1].length(), words[i].length()))
                if (dict[words[i-1].charAt(j) - 'a'] < dict[words[i].charAt(j) - 'a'])
                    break;
                else if (dict[words[i-1].charAt(j) - 'a'] > dict[words[i].charAt(j) - 'a'])
                    return false;
                else
                    j++;
            if (j == words[i].length() && j < words[i - 1].length()) return false;
        }
        return true;
    }
```

Solution中用了一个`continue search`去解决中间的判断。

```java
public boolean isAlienSorted(String[] words, String order) {
        int[] index = new int[26];
        for (int i = 0; i < order.length(); ++i)
            index[order.charAt(i) - 'a'] = i;

        search: for (int i = 0; i < words.length - 1; ++i) {
            String word1 = words[i];
            String word2 = words[i+1];

            // Find the first difference word1[k] != word2[k].
            for (int k = 0; k < Math.min(word1.length(), word2.length()); ++k) {
                if (word1.charAt(k) != word2.charAt(k)) {
                    // If they compare badly, it's not sorted.
                    if (index[word1.charAt(k) - 'a'] > index[word2.charAt(k) - 'a'])
                        return false;
                    continue search;
                }
            }

            // If we didn't find a first difference, the
            // words are like ("app", "apple").
            if (word1.length() > word2.length())
                return false;
        }

        return true;
    }
```
