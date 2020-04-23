# 5. Longest Palindromic Substring

## 题目

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

>**示例 1：**
>
>>**输入:** "babad"  
>>**输出:** "bab"  
>>**注意:** "aba" 也是一个有效答案。  
>
>**示例 2：**
>
>>输入: "cbbd"  
>>输出: "bb"

## 解法

### 1 动态规划判断回文串

令dp[i][j]判断从i到j的字符串是否是回文的，那么状态转移方程是
```
dp[i][j] = true if (dp[i+1][j-1] && s[i]==s[j])
```

边界条件需要多考虑一下：  
如果`i==j`表示字符串只有一个字符，肯定是回文串；  
如果`j-i == 1 || 2`,那么判断`s[i] == s[j]`是否为真即可。

状态转移方程改写为
```
dp[i][j] = true if ((j - i < 2 || dp[i+1][j-1]) && s[i] == s[j])
```

统计dp矩阵的上三角即可。时间复杂度O(n^2)，空间复杂度O(n^2)

```java
public String longestPalindrome(String s) {
        String ans= "";
        int maxLen = 0, n = s.length();
        boolean[][] dp = new boolean[n][n];
        for (int j = 0; j< n; j++){
            for (int i = j; i>=0; i--){
                if (s.charAt(i) == s.charAt(j) && (j - i < 2 || dp[i+1][j-1])){
                    dp[i][j] = true;
                    if (j - i >= maxLen){
                        ans = s.substring(i, j + 1);
                        maxLen = j - i + 1;
                    }
                }
            }
        }
        return ans;
    }
```

### 2 中心两端扩展

```java
public String longestPalindrome(String s) {
        if (s.length() == 0 || s == null) return "";
        int n = s.length() ,maxLen = 0, start = 0, end = 0;
        for (int center = 0; center < 2 * n - 1; center++){
            int left = center / 2;
            int right = left + center % 2;
            while (left>=0 && right < n && s.charAt(left) == s.charAt(right)){
                if (right - left >= maxLen){
                    maxLen = right - left + 1;               
                    start = left;
                    end = right;
                }
                left--;
                right++;
            }
        }
        return s.substring(start, end+1);
    }
```

### 3 骚气的2ms解法

```java
public String longestPalindrome(String s) {
        String result = "";
        int[] limit = {0, 0};
        char[] ch = s.toCharArray();
        int i = 0;
        while (i < ch.length) {
            i = indexOf(ch, i, limit);
        }
        result = s.substring(limit[0], limit[1]);
        return result;
    }
    
    public int indexOf(char[] ch, int low, int[] limit) {
        int high = low + 1;
        while (high < ch.length && ch[high] == ch[low]) {
            high++;
        }
        int result = high;
        while (low > 0 && high < ch.length && ch[low - 1] == ch[high]) {
            low--;
            high++;
        }

        if (high - low > limit[1] - limit[0]) {
            limit[0] = low;
            limit[1] = high;
        }
        return result;
    }
```