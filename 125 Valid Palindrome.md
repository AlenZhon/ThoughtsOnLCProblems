# 125 Valid Palindrome

## 题目描述

给定一字符串，在忽略其中非数字字母[0-9a-zA-Z]的其他字符，且忽略字母大小写的情况下，判断该字符串是否回文。

>Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
>
>**Note**: For the purpose of this problem, we define empty string as valid palindrome.
>
>Example 1:
>
>**Input**: "A man, a plan, a canal: Panama"  
>**Output**: true
>
>Example 2:
>
>**Input**: "race a car"  
>**Output**: false

## 怎么解的

一开始还想String类里有没有`.reverse()`方法。

不如自己设置首尾两个下标，判断是否在`[0-9a-zA-Z]`，然后比较两个下标所在的字符是否相等。时间复杂度O(n)，空间O(1)。

```java
public boolean isPalindrome(String s) {
        if (s == "") return true;
        int i = 0 , j = s.length() -1;
        while (i<j) {
            while (i<j && !((s.charAt(i)>='a' && s.charAt(i)<='z')
                           ||(s.charAt(i)>='A' && s.charAt(i)<='Z')
                           ||(s.charAt(i)>='0' && s.charAt(i)<='9'))) {
                i++;
            }
            while (i<j && !((s.charAt(j)>='a' && s.charAt(j)<='z')
                           ||(s.charAt(j)>='A' && s.charAt(j)<='Z')
                           ||(s.charAt(j)>='0' && s.charAt(j)<='9'))) {
                j--;
            }
            if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
```

## Notes

- 如果输入的字符串没有数字或字母，该字符串仍然看做是回文。
- 比较时注意大小写的转换。`Character.toLowerCase()` 方法是`public static char` 修饰的。如果用`String.toLowerCase()`会报类型转换错误。
- 有没有更简洁的方法判断`s.charAt(i)`在不在需要的`[0-9a-zA-Z]`范围里呢？
