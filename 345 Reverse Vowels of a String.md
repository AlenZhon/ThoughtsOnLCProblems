# 345. Reverse Vowels of a String

## 题目

给定一个字符串，保留辅音的顺序，将里面的元音字母首尾交换后输出。

>Write a function that takes a string as input and reverse only the vowels of a string.
>
>**Example 1:**
>
>>Input: "hello"  
>>Output: "holle"
>
>**Example 2:**
>
>>Input: "leetcode"  
>>Output: "leotcede"
>
>**Note:**
>The vowels does not include the letter "y".

## 解法

把String转成数组，将元音字母预先存储，头尾指针比较。

```java
private final HashSet vowels = new HashSet<>(Arrays.asList('a','e','i','o','u','A','E','I','O','U'));
    public String reverseVowels(String s) {
        char[] c = s.toCharArray();
        int head = 0, tail = c.length - 1;
        while (head < tail) {
            boolean h = vowels.contains(c[head]), t = vowels.contains(c[tail]);
            if (h && t) {
                char temp = c[head];
                c[head] = c[tail];
                c[tail] = temp;
                head++;
                tail--;
            } else {
                if (!t) tail--;
                if (!h) head++;
            }
        }
        return String.valueOf(c);
    }
```

另一种方法的代码更简练，不使用HashSet而是使用boolean[] vowels。

```java
public String reverseVowels(String s) {
         boolean[] vowels = new boolean[256];
        char[] chars = s.toCharArray();
        for (char c : "aeiouAEIOU".toCharArray())
            vowels[c] = true;

        for (int l = 0, r = chars.length - 1; l < r; l++, r--) {
            while (l < r && !vowels[chars[l]]) l++;
            while (l < r && !vowels[chars[r]]) r--;
            char temp = chars[l];
            chars[l] = chars[r];
            chars[r] = temp;
        }
        return String.valueOf(chars);

    }
```
