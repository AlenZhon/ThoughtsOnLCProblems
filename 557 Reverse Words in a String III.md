# 557. Reverse Words in a String III

## 题目

将一个英文句子里每个用空格分开的字符串按字符翻转。

>Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.
>
>Example 1:
>
>>Input: "Let's take LeetCode contest"
>>Output: "s'teL ekat edoCteeL tsetnoc"
>
>Note: In the string, each word is separated by single space and there will not be any extra space in the string.

## 解法

也是水题。Note里保证了空格是单空格所以很简单。如果有多个空格的话还得把注释的那一句话加上。时间复杂度和空间复杂度均为O(n)。

```java
public String reverseWords(String s) {
        char[] c = s.toCharArray();
        int i = 0, j = 0;
        while (i < c.length) {
            //for (;i < c.length && c[i] == ' '; i++);
            for (j = i; j < c.length && c[j] != ' '; j++);
            int tail = j - 1;
            while (i< tail) {
                char temp = c[i];
                c[i++] = c[tail];
                c[tail--] = temp;
            }
            i = j+1;
        }
        return new String(c);
    }
```

中间变量j的for循环也可调用`String.indexOf(" ", i)`代替。

```java
public String reverseWords(String s) {
        char[] c = s.toCharArray();
        int i = 0;
        while (i < c.length) {
            int j = s.indexOf(" ", i);
            if (j < 0) j = c.length;
            int tail = j - 1;
            while (i < tail) {
                char temp = c[i];
                c[i++] = c[tail];
                c[tail--] = temp;
            }
            i = j + 1;
        }
        return new String(c);
    }
```

如果直接使用StringBuilder和它自带的reverse()方法，代码更加简洁。时间和空间复杂度均为O(n).

```java
String[] words = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for (String word : words)
            sb.append(new StringBuilder(word).reverse().toString() + " ");
        return sb.toString().trim();
```
