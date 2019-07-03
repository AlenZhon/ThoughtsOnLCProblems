# 3 Longest Substring without Repeating Characters

## 题目描述

Given a string, find the length of the longest substring without repeating characters.

Example 1:
>**Input:** "abcabcbb"
>**Output:** 3
>**Explanation:** The answer is "abc", with the length of 3.

Example 2:
>**Input:** "bbbbb"
>**Output:** 1
>**Explanation:** The answer is "b", with the length of 1.

Example 3:
>**Input:** "pwwkew"
>**Output:** 3
>**Explanation:** The answer is "wke", with the length of 3.

Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## 解题思路

构造滑动窗口，下标为index1 index2，每次比较滑动窗口后一个字母是否与窗口内字母相等，如果在则将index1移到窗口字母的下标处。

若不相等则比较maxlength与滑动窗口长度， 记下最大者。

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int index1 = 0, index2 =1, maxlength = 1;
        if (s.isEmpty()) {return 0;}
        while (index2 <s.length()) {
            temp_s = s.substring(index1, index2);
            char c = s.charAt(index2);
            repeat_index = checkrepeat(temp_s, index1, c);
            if (repeat_index == -1) {
                maxlength = Math.max(maxlength, index2 - index1 + 1);
            }else {
                index1 = repeat_index +1;
            }
            index2 +=1;
        }
        return maxlength;
    }
    int checkrepeat(String str, int index, char target) {
            for (int i =0; i<str.length(); i++) {
                if (str.charAt(i) == target) {
                    return (index + i);
                }
            }
            return -1;
    }
}

```

运行时间5ms，和Solution 中Approach3: Sliding Window Optimized的想法较为一致，但它使用了HashMap或index字符数组（index 数组的时间复杂度是O(n),空间复杂度O(m)与字符集大小有关。把代码放进去跑，它的Runtime 2ms，然而HashMap的示例Runtime 7ms???）

>(Instead of using a set to tell if a character exists or not, we could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character)
