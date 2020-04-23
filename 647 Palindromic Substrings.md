# 647. Palindromic Substrings

## 题目

给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。

**示例 1:**

>输入: "abc"  
>输出: 3  
>解释: 三个回文子串: "a", "b", "c".

**示例 2:**
>
>输入: "aaa"  
>输出: 6  
>说明: 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".

**注意:**

输入的字符串长度不会超过1000。

## 解法

### 1 中间向两端延伸

一个长度为n 的字符串，可能出现的回文串中心有2*n - 1个：字母和字母之间的空隙。

用left和right尽量向左右两端展开，判断原子串加上新进来的两个字符构不构成回文串。

时间复杂度O(n^2)，空间复杂度O(1)

```java
public int countSubstrings(String s) {
        int ans = 0, n = s.length();
        for (int center = 0; center < 2 * n - 1; center++){
            int left = center / 2;
            int right = left + center % 2; // 当中心是两个字母的间歇时i%2 = 1；当中心是字母时 left==right都落在该字母的位置
            while (left >=0 && right < n && s.charAt(left) == s.charAt(right)){
                ans++;
                left--;
                right++;
            }
        }
        return ans;
    }
```

### 2 动态规划

令dp[i][j]判断从i到j的字符串是否是回文的，那么状态转移方程是
```
dp[i][j] = true if (dp[i+1][j-1] && s[i]==s[j])
```

边界条件需要多考虑一下：  
如果i==j表示字符串只有一个字符，肯定是回文串；  
如果`j-i == 1 || 2`,那么判断`s[i] == s[j]`是否为真即可。

状态转移方程改写为
```
dp[i][j] = true if ((j - i < 2 || dp[i+1][j-1]) && s[i] == s[j])
```

统计dp矩阵的上三角即可。时间复杂度O(n^2)，空间复杂度O(n^2)

```java
public int countSubstrings(String s) {
        int ans = 0;
        char[] c = s.toCharArray();
        boolean[][] dp = new boolean[c.length][c.length];
        for (int j =0; j< c.length; j++){  //right
            for (int i = j; i>=0; i--){  //left
                if (c[i] == c[j] && (j - i < 2 || dp[i+1][j-1])){
                    dp[i][j] = true;
                    ans++;
                }    
            }
        }
        return ans;
    }
```
