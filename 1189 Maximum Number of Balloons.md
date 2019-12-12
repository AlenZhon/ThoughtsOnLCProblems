# 1189. Maximum Number of Balloons

## 题目

给一个只包含小写字母字符串，用里面的字母组成`"balloon"`这个英文单词。每个字母只能用一次，问最多能组成多少个`"balloon"`。

>Given a string text, you want to use the characters of text to form as many instances of the word "balloon" as possible.
>
>You can use each character in text at most once. Return the maximum number of instances that can be formed.
>
>**Example 1:**
>
>>Input: text = "nlaebolko"  
>>Output: 1
>
>**Example 2:**
>
>>Input: text = "loonbalxballpoon"  
>>Output: 2  
>
>**Example 3:**
>
>>Input: text = "leetcode"  
>>Output: 0
>
>**Constraints:**
>
> - 1 <= text.length <= 10^4
> - text consists of lower case English letters only.

## 解法

统计字符频次的水题。时间复杂度O(n)，空间O(1)。

```java
public int maxNumberOfBalloons(String text) {
        int[] ch = new int[5];
        for (char c : text.toCharArray())
            switch (c){
                case 'b' : ch[0]++; break;
                case 'a' : ch[1]++; break;
                case 'l' : ch[2]++; break;
                case 'o' : ch[3]++; break;
                case 'n' : ch[4]++; break;
            }
        int numBAN = Math.min(Math.min(ch[0], ch[1]), ch[4]);
        int numLO = Math.min(ch[2], ch[3]);
        return Math.min(numBAN, numLO / 2);
    }
```
