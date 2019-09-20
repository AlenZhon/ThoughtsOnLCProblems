# 434. Number of Segments in a String

## 题目

返回一个字符串的segment个数，一个segment定义为一个由非空格字符组成的连续子串。

>Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.
>
>Please note that the string does not contain any non-printable characters.
>
>**Example:**
>
>>Input: "Hello, my name is John"  
>>Output: 5

## 解法

用了自带的函数`trim()` `split()` `length()`。
要考虑边界条件，比如原字符串就是一连串空格应当输出0.

两个segment之间可能由若干个空格隔开，适合用`\\s+`表示。（之前用`" "` 被测试用例教做人。）

```java
public int countSegments(String s) {
        s = s.trim();
        if (s.length() == 0)  return 0;
        return s.split("\\s+").length;
    }
```

时间复杂度O(n)(java的built-in函数基本上时间复杂度为O(n)或O(1))，空间复杂度O(n)（`split()`返回一个O(n)长度的`array/list`）

如果空间复杂度需要控制在O(1)，可以遍历字符串寻找空格与非空格字符之间的间隙。

```java
public int countSegments(String s) {
        int count =0;
        for (int i =0; i< s.length(); i++) {
            if ((i==0 || s.charAt(i-1) ==' ') && s.charAt(i) != ' ')
                count++;
        }
        return count;
    }
```