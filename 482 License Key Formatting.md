# 482. License Key Formatting

## 题目

给定一个字符串，由英文字母、数字以及短横线(-)组成。给定数字K，将原字符串由后向前每K个字母/数字组成一组，每组之间用短横线连接。最靠近开头的一组可以由小于K个字符组成。最后返回新字符串的大写形式。

>You are given a license key represented as a string S which consists only alphanumeric character and dashes. The string is separated into N+1 groups by N dashes.
>
>Given a number K, we would want to reformat the strings such that each group contains exactly K characters, except for the first group which could be shorter than K, but still must contain at least one character. Furthermore, there must be a dash inserted between two groups and all lowercase letters should be converted to uppercase.
>
>Given a non-empty string S and a number K, format the string according to the rules described above.
>
>**Example 1:**
>
>>Input: S = "5F3Z-2e-9-w", K = 4
>>
>>Output: "5F3Z-2E9W"
>>
>>Explanation: The string S has been split into two parts, each part has 4 characters.
Note that the two extra dashes are not needed and can be removed.
>
>**Example 2:**
>
>>Input: S = "2-5g-3-J", K = 2
>>
>>Output: "2-5G-3J"
>>
>>Explanation: The string S has been split into three parts, each part has 2 characters except the first part as it could be shorter as mentioned above.
>
>**Note**:
>
>- The length of string S will not exceed 12,000, and K is a positive integer.
> - String S consists only of alphanumerical characters (a-z and/or A-Z and/or 0-9) and dashes(-).
> - String S is non-empty.

## 解法

暂时没有什么好想法，构造一个`StringBuilder`，从后向前添加字符串的每一位，在合适的时间判断要不要加连接线。最后一个 `reverse().toString().toUpperCase()`

```java
public String licenseKeyFormatting(String S, int K) {
        StringBuilder sb = new StringBuilder();
        int count = 0;
        for (int i = S.length() - 1; i>=0; i--){
            char ch = S.charAt(i);
            if (ch == '-') continue;
            if (count == K){
                sb.append('-');
                count =0;
            }
            sb.append(ch);
            count++;
        }
        return sb.reverse().toString().toUpperCase();
    }
```

讨论区里有人用 `sb.length() % (K+1) == K`判断要加连接线。然后也可以在for 循环里先用`Character.toUpperCase(char ch)`转成大写字母。

OJ 上的运行时间20ms，考虑如果提前安排存储空间会不会省去StringBuilder的append时间。

```java
public String licenseKeyFormatting(String S, int K) {
        final String str = S.toUpperCase().replace("-","");
        int len1 = str.length(), count = 0;
        if (len1 == 0) return str;
        int n = len1 % K == 0 ? len1 + len1 / K - 1 : len1 + len1 / K;
        char[] ch = new char[n];
        for (int i = len1 -1, j = n -1; i >=0; j--) {
            if (count == K) {
                ch[j] = '-';
                count = 0;
            } else {
                ch[j] = str.charAt(i--);
                count++;
            }
        }
        return new String(ch);
    }
```

运行时间13ms。

submission里运行时间最快的想法也是使用了`char[] array`，不过安排了比输出字符串大小更大的存储空间，并安排下标存储最终长度。

```java
public String licenseKeyFormatting(String S, int K) {
        if(S == null ||S.length() == 0) return S;
        int len = S.length() / K + S.length();
        if(S.length() % K == 0) len--;
        char[] array = new char[len];
        int j = len - 1;
        int counter = 0;
        for(int i = S.length() - 1; i >= 0; i--) {
            char c = S.charAt(i);
            if(c != '-') {
                if(c >= 'a') c = (char) ('A' + c - 'a');
                array[j--] = c;
                counter++;
                if(counter == K && i != 0) {
                    array[j--] = '-';
                    counter = 0;
                }
            }
        }
        if(j + 1 < len && array[j + 1] == '-') j++;
        return new String(array, j + 1, len - j - 1);
    }
```
