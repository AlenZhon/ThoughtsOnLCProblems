# 1221. Split a String in Balanced Strings

## 题目

一个 *balanced*字符串里只包含 `L` 和 `R`，且两个字母的出现次数相同。  
现在要将这个字符串切成若干个子字符串，要求每个子字符串都是 *balanced*字符串。求最多能切出的 *balanced*子字符串个数。

>*Balanced* strings are those who have equal quantity of 'L' and 'R' characters.
>
>Given a balanced string s split it in the maximum amount of balanced strings.
>
>Return the maximum amount of splitted balanced strings.
>
>**Example 1:**
>
>>Input: s = "RLRRLLRLRL"  
>>Output: 4  
>>Explanation: s can be split into "RL", "RRLL", "RL", "RL", each substring contains same number of 'L' and 'R'.
>
>**Example 2:**
>
>>Input: s = "RLLLLRRRLR"  
>>Output: 3
>>Explanation: s can be split into "RL", "LLLRRR", "LR", each substring contains same number of 'L' and 'R'.
>
>**Example 3:**
>
>>Input: s = "LLLLRRRR"  
>>Output: 1  
>>Explanation: s can be split into "LLLLRRRR".
>
>**Example 4:**
>
>>Input: s = "RLRRRLLRLL"  
>>Output: 2  
>>Explanation: s can be split into "RL", "RRRLLRLL", since each substring contains an equal number of 'L' and 'R'
>
>**Constraints:**
>
> - 1 <= s.length <= 1000
> - s[i] = 'L' or 'R'

## 解法

定义一个变量，遍历字符串遇到R该变量自增，遇到L自减。每次变量为0时说明遇到了一个子字符串。

```java
public int balancedStringSplit(String s) {
        int cut = 0, numRL = 0;
        for (char c : s.toCharArray()){
            if (c == 'R') numRL++;
            else if (c == 'L') numRL--;
            if (numRL == 0) cut++;
        }
        return cut;
    }
```
