# 58 Length of Last Word

## 题目描述

>Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.
>
>If the last word does not exist, return 0.
>
>Note: A word is defined as a character sequence consists of non-space characters only.
>
>**Example:**
>
>**Input:** "Hello World"  
>**Output:** 5

## 怎么解的

```java
String[] substr = s.split(" ");
return (substr.length == 0) ? 0 : substr[substr.length -1].length();
```

结果发现时间略慢一点点，只击败了46.37%的提交。 于是看了一下0ms的submission——他们用的是trim()和lastIndexOf()。

```java
s = s.trim();
return s.length() - s.lastIndexOf(" ") - 1;
```
