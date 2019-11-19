# 925. Long Pressed Name

## 题目

你朋友在电脑上输入用户名，不过电脑键盘比较烂，有可能按一个a会输出好几个a。现在给定正确的用户名`name`和你朋友用这个键盘输入的用户名`typed`两个字符串，判断`typed`有没有可能是你朋友的用户名，其中有些字母（也可能没有）重复输出了好几次。

>Your friend is typing his name into a keyboard.  Sometimes, when typing a character c, the key might get long pressed, and the character will be typed 1 or more times.
>
>You examine the typed characters of the keyboard.  Return True if it is possible that it was your friends name, with some characters (possibly none) being long pressed.
>
>**Example 1:**
>
>>Input: name = "alex", typed = "aaleex"  
>>Output: true  
>>Explanation: 'a' and 'e' in 'alex' were long pressed.
>
>**Example 2:**
>
>>Input: name = "saeed", typed = "ssaaedd"  
>>Output: false  
>>Explanation: 'e' must have been pressed twice, but it wasn't in the typed output.
>
>**Example 3:**
>
>>Input: name = "leelee", typed = "lleeelee"  
>>Output: true
>
>**Example 4:**
>
>>Input: name = "laiden", typed = "laiden"  
>>Output: true  
>>Explanation: It's not necessary to long press any character.
>
>**Note:**
>
> - `name.length <= 1000`
> - `typed.length <= 1000`
> - The characters of name and typed are lowercase letters.

## 解法

可以用two-pointer解决，时间复杂度O(N2)，空间复杂度O(1)，N2为`typed.length`。

初始化i, j分别为name typed的遍历指针。

如果两指针指向的字符相同则都自增1;  
不同，则判断如果`name[i - 1] == typed[j]`，说明出现了长按字母的情况;  
如果连这都不相等，说明出现了`name`里没有的字符，返回false。  
最后判断typed字符串的结尾多余的字符中有没有name里没出现的字符(`"alex", "aleexxxt"`)

```java
public boolean isLongPressedName(String name, String typed) {
        if (name.length() > typed.length()) return false;
        if (name.length() == 0 ) return true;
        int i = 0 , j = 0;
        while (i< name.length() && j < typed.length()) {
            if (name.charAt(i) == typed.charAt(j)){
                i++;
                j++;
            } else if (i > 0 && name.charAt(i - 1) == typed.charAt(j))
                j++;
            else
                return false;
        }
        if (i == name.length() && j > 0)
            while (j < typed.length() && typed.charAt(j) == typed.charAt(j - 1)) j++;
        return (j == typed.length() && i == name.length());
    }
```
