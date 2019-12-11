# 1170. Compare Strings by Frequency of the Smallest Character

## 题目

定义函数`f(String s)`为字符串s中最小字符的出现次数。例如`f("dcce") = 2`因为`c`出现了两次。

现在给定两个数组`String[] queries`和`String[] words`。要求返回数组answer，其中answer[i]为满足`f(queries[i]) < f(Word) where Word is in words` 的 `word`个数。

>Let's define a function `f(s)` over a non-empty string `s`, which calculates the frequency of the smallest character in `s`. For example, if `s = "dcce"` then `f(s) = 2` because the smallest character is `"c"` and its frequency is 2.
>
Now, given string arrays `queries` and `words`, return an integer array `answer`, where each `answer[i]` is the number of words such that `f(queries[i]) < f(W)`, where `W` is a word in `words`.
>
>**Example 1:**
>
>>Input: `queries = ["cbd"]`, `words = ["zaaaz"]`  
>>Output: `[1]`  
>>Explanation: On the first query we have `f("cbd") = 1, f("zaaaz") = 3` so `f("cbd") < f("zaaaz")`.
>
>**Example 2:**
>
>>Input: `queries = ["bbb","cc"]`, `words = ["a","aa","aaa","aaaa"]`  
>>Output: `[1,2]`  
>>Explanation: On the first query only `f("bbb") < f("aaaa")`. On the second query both `f("aaa")` and `f("aaaa")` are both greater than `f("cc")`.
>
>**Constraints:**
>
> - 1 <= queries.length <= 2000
> - 1 <= words.length <= 2000
> - 1 <= queries[i].length, words[i].length <= 10
> - queries[i][j], words[i][j] are English lowercase letters.

## 解法

按照题目的直接题意，计算`queries[i]`, `words[i]`分别计算`f()`。然后把`f(words[i])`排序，然后二分查找看有几个数小于`f(queries[i])`。  
二分查找的取等条件真的要注意一下。

```java
public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] wordsCount = new int[words.length];
        for (int i = 0; i< words.length; i++)
            wordsCount[i] = countWords(words[i]);
        Arrays.sort(wordsCount);
        int[] ret = new int[queries.length];
        for (int i = 0; i < queries.length; i++){
            int qCount = countWords(queries[i]);
            ret[i] = binarySearch(qCount, wordsCount);
        }
        return ret;
    }
    private int binarySearch(int x, int[] count){
        int left = 0, right = count.length - 1;
        while (left <= right){
            int mid = left + (right - left) / 2;
            if (x >= count[mid])
                left = mid + 1;
            else
                right = mid - 1;
        }
        return count.length - left;
    }

    private int countWords(String word){
        char ch = 'z';
        int count = 0;
        for (char c : word.toCharArray())
            if (c < ch){
                ch = c;
                count = 1;
            } else if (c == ch)
                count++;
        return count;
    }
```

由于`Constraint`里有约束条件，使得每个字符串的长度都在`[1, 10]`以内。如此一来，`f()`函数的值域也在此范围以内，可以直接定义int[11]记录下`f()`值的出现频次，然后把int[11]的出现频次变成累积分布函数。从而绕过了排序和二分查找。

```java
public int[] numSmallerByFrequency(String[] queries, String[] words) {
        int[] wordsCount = new int[11];
        for (int i = 0; i< words.length; i++){
            int count = countWords(words[i]);
            wordsCount[count]++;
        }
        int sum = 0;
        for (int i = 0; i< 11; i++){
            sum += wordsCount[i];
            wordsCount[i] = sum;
        }

        int[] ret = new int[queries.length];
        for (int i = 0; i < queries.length; i++){
            int qCount = countWords(queries[i]);
            ret[i] = wordsCount[wordsCount.length - 1] - wordsCount[qCount];
        }
        return ret;
    }

    private int countWords(String word){
        int[] count = new int[26];
        for (char c : word.toCharArray())
            count[c - 'a']++;
        for (int i =0; i< 26; i++)
            if (count[i] > 0)
                return count[i];
        return 0;
    }
```
