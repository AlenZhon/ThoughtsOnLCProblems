# 409. Longest Palindrome

## 题目

给定一个字符串，从这个字符串中取出字母构成回文串，求能构成回文串的最大长度。（大小写敏感）

>Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.
>
>This is case sensitive, for example "Aa" is not considered a palindrome here.
>
>**Note:**
>Assume the length of given string will not exceed 1,010.
>
>**Example:**
>
>>**Input:** "abccccdd"
>>**Output:** 7
>
>**Explanation:**
>One longest palindrome that can be built is "dccaccd", whose length is 7.

## 解法

首先肯定是统计字符串中的字母出现次数。回文字符串需要成对的字母，最后看需不需要在最中间加一个字母。

所以一开始是这么写的：

```java
for (int count : dict){
  if (count % 2 == 0) maxLength+=count;
  if (count == 1 ) singleChar = 1;
}
return maxLength + singleChar;
```

然而这样没有考虑到字母出现奇数次的情况如 `"ccc"` 。

考虑有没有一个迭代的通项公式。写了几项得出下面的式子，解决了奇数次的情况，但是对字母出现的顺序考虑不周（`"ccd"`时， maxLength在d处不更新），`count`比较最大值没有什么意义。

```java
for (int count: dict) {
  maxLength = Math.max(count, maxLength + count / 2 *2);
}
return maxLength;
```

修改程序，每次自增 `count//2 *2` （取`count//2`对字母），并判断如果`count` 是奇数并且`maxLength`现在是偶数，则再加一（把`count`的所有字母都用上）。

```java
public int longestPalindrome(String s) {
        if (s.length() == 0) return 0;
        int[] dict = new int[128];
        for (char ch : s.toCharArray())
            dict[ch]+=1;
        int maxLength = 0;
        for (int count : dict) {
            maxLength += count / 2 *2;
            if ( maxLength %2 == 0 && count %2 ==1)
                maxLength++;
        }
        return maxLength;
    }
```

由于需要统计频次，时间复杂度O(N)。空间复杂度O(1)

评论区大佬统计出现了奇数次的字母个数`single`。回文串的字母个数与`single`有关。如果`single` = 0或1，则原字符串所有字母都用在了回文串里。如果`single` > 1，则回文串字母个数比原字符串少(`single - 1`)

```java
public int longestPalindrome(String s) {
        int[] chars = new int[128];
        char[] t = s.toCharArray();
        for(char c:t){
            chars[c]++;
        }
        int single = 0;
        for(int n:chars){
            if(n%2!=0){
                single++;
            }
        }
        return single > 1 ? t.length-single+1 :t.length;
    }
```
