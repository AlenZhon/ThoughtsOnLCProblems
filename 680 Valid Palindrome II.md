# 680. Valid Palindrome II

## 题目

给定一个字符串，条件是至多删除其中的一个字符，判断能否将这个字符串变成回文字符串。

>Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.
>
>Example 1:
>>
>>Input: "aba"  
>>Output: True  
>
>Example 2:
>
>>Input: "abca"  
>>Output: True
>>Explanation: You could delete the character 'c'.
>
>Note:
>
> - The string will only contain lowercase characters a-z. The maximum length of the string is 50000.

## 解法

用了个count变量记录跳过的字符数。i,j两个指针从首尾向中间移动。如果遇到了不相等的情况，判断是i向后移还是j向前移。

按照`abcddba`的例子想，可以比较`s[i+1] == s[j]` 或者是`s[i] ==s[j+1]` 。所以一开始是这么写的：

```java
public boolean validPalindrome(String s) {
        if (s.length() == 0) return true;
        int i = 0, j = s.length() - 1, count = 0;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                if (count > 0) return false;
                count++;
                if (s.charAt(i + 1) == s.charAt(j)) {
                    i++;
                    continue;
                } else if (s.charAt(j - 1) == s.charAt(i)) {
                    j--;
                    continue;
                } else
                    return false;
            }
            i++;
            j--;
        }
        return true;
    }
```

提交上去报错了。实际上这两个条件并不是答案的充要条件。考虑测试用例`"lcupuupucul"`，当i指向第二个字母c时，`s[i+1] == s[j]`但我们可以看到删掉j指向的u就可以构成回文串。

所以当判断到 `(s.charAt(i) != s.charAt(j))` 时，直接判断 `[i+1, j]`或者`[i, j-1]` 是否回文。

```java
public boolean validPalindrome(String s) {
        if (s.length() == 0) return true;
        int i = 0, j = s.length() - 1, count = 0;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return isPalindrome(s, i+1, j) || isPalindrome(s, i, j-1);
            }
            i++;
            j--;
        }
        return true;
    }

    private boolean isPalindrome(String s, int start, int end) {
        for (int i = start; i <= start + (end - start) /2; i++ )
            if (s.charAt(i) != s.charAt(end - i + start)) return false;
        return true;
    }
```

时间复杂度O(n) 空间复杂度O(1)

如果把`String`先转成`charArray` 可能会减少一些反复调用`charAt()`的运行时间。
