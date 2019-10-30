# 696. Count Binary Substrings

## 题目

给定一个只包含0和1的字符串，计算其中满足下列条件的子串的个数：该子串中0和1连续排列，且个数相等（如  `01`,`10`,`0011`,`1100`）。重复出现的子串按照出现次数计算。

>Give a string s, count the number of non-empty (contiguous) substrings that have the same number of 0's and 1's, and all the 0's and all the 1's in these substrings are grouped consecutively.
>
>Substrings that occur multiple times are counted the number of times they occur.
>
>**Example 1:**
>
>>Input: `"00110011"`
>>Output: 6  
>>Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: `"0011", "01", "1100", "10", "0011", and "01"`.
>>
>>Notice that some of these substrings repeat and are counted the number of times they occur.
>>
>>Also, `"00110011"` is not a valid substring because all the 0's (and 1's) are not grouped together.
>
>**Example 2:**
>
>>Input: `"10101"`
>>Output: 4
>>Explanation: There are 4 substrings: `"10", "01", "10", "01"` that have equal number of consecutive 1's and 0's.
>
>**Note:**
>
> - s.length will be between 1 and 50,000.
> - s will only consist of "0" or "1" characters.

## 解法

考虑一个满足条件的子串`11110000`，其中还包含着3个满足条件的子串。可以看出子串的个数和连续0，连续1的个数有关。记上一个连续字符（0或1）的个数为`prev`，当前连续字符的个数为`cur`，则可以形成`Math.min(prev, cur)`个满足条件的字符串。

由于重复出现的字符串重复计数，所以只需遍历一次即可。时间复杂度O(s.length())，空间O(1)。

```java
public int countBinarySubstrings(String s) {
        int count = 0, prev = 0, cur = 1;
        for (int i = 1; i< s.length(); i++) {
            if (s.charAt(i) != s.charAt(i - 1)) {
                count+= Math.min(prev, cur);
                prev = cur;
                cur = 1;
            } else
                cur++;
        }
        return count + Math.min(prev, cur);
    }
```
