# 748. Shortest Completing Word

## 题目

`String licensePlate` 由大小写字母，数字和空格组成，为方便可以将里面的字母全部看做小写。在`String`数组`words`中找到能覆盖`licensePlate`中所有字母的最短字符串。

注意，如果`licensePlate`中字母重复`n`次，则`words`中的元素里该字母最少也要重复`n`次。

> Find the minimum length word from a given dictionary `words`, which has all the letters from the string `licensePlate`. Such a word is said to complete the given string `licensePlate`
>
>Here, for letters we ignore case. For example, "`P`" on the `licensePlate` still matches "`p`" on the word.
>
>It is guaranteed an answer exists. If there are multiple answers, return the one that occurs first in the array.
>
>The license plate might have the same letter occurring multiple times. For example, given a licensePlate of "`PP`", the word "`pair`" does not complete the `licensePlate`, but the word "`supper`" does.
>
>**Example 1:**
>
>>Input: licensePlate = "1s3 PSt", words = `["step", "steps", "stripe", "stepple"]`  
>>Output: "`steps`"  
>>Explanation: The smallest length word that contains the letters "`s`", "`p`", "`s`", and "`t`".  
Note that the answer is not "`step`", because the letter "`s`" must occur in the word twice.
Also note that we ignored case for the purposes of comparing whether a letter exists in the word.
>
>**Example 2:**
>
>>Input: licensePlate = "1s3 456", words = `["looks", "pest", "stew", "show"]`  
>>Output: "`pest`"
>>Explanation: There are 3 smallest length words that contains the letters "`s`".
We return the one that occurred first.
>
>**Note:**
>
> - `licensePlate` will be a string with length in range `[1, 7]`.
> - `licensePlate` will contain digits, spaces, or letters (uppercase or lowercase).
> - `words` will have a length in the range `[10, 1000]`.
> - Every `words[i]` will consist of lowercase letters, and have length in range `[1, 15]`.

## 解法

没想到什么骚方法，直接撸。把`licensePlate`用一个`int[26]`数组记录字母出现频次（不区分大小写）。然后遍历`words`，如果这个`word`覆盖了所有的字母次数（即`hasAllChar(letters, word)`）并且长度更小，就更新`retIndex`。

```java
public String shortestCompletingWord(String licensePlate, String[] words) {
        int[] letters = new int[26];
        int letterLen = 0, minLen = Integer.MAX_VALUE, retIndex = -1, i = -1;
        for (char c : licensePlate.toCharArray()) {
            if (c >='a' && c<='z') {letters[c - 'a']++; letterLen++;}
            if (c >='A' && c<='Z') {letters[c - 'A']++; letterLen++;}
        }
        for (String word : words) {
            i++;
            if (word.length() < letterLen) continue;
            if (word.length() < minLen && hasAllChar(letters, word)) {
                retIndex = i;
                minLen = word.length();
            }
        }
        return words[retIndex];
    }

    private boolean hasAllChar(int[] letter, String word) {
        int[] maps = new int[26];
        System.arraycopy(letter, 0, maps, 0, 26); //deep copy
        for (char c : word.toCharArray())
            if (maps[c - 'a'] > 0)
                maps[c - 'a']--;
        for (int i : maps)
            if (i > 0) return false;
        return true;
    }
```

子函数每次进来就要深拷贝一下`letter[]`数组。修改逻辑，用maps记录word的字母出现频次，然后逐个和letter[]比较。

```java
private boolean hasAllChar(int[] letter, String word) {
    int[] temp = new int[26];
    for (char c : word.toCharArray())
      temp[c - 'a']++;

    for (int i = 0; i < 26; i++)
      if (letter[i] > 0 && letter[i] > temp[i])
        return false;
    return true;
}
```
