# 6. ZigZag Conversion

## 题目

给定一个字符串S和行数，要把它zigzag写出来之后重新按行输出。

>The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
>
>>```java
>>P   A   H   N  
>>A P L S I I G  
>>Y   I   R  
>>```
>
>And then read line by line: "`PAHNAPLSIIGYIR`"
>
>Write the code that will take a string and make this conversion given a number of rows:
>
>`string convert(string s, int numRows);`
>
>**Example 1:**
>>
>>Input: s = "`PAYPALISHIRING`", numRows = 3  
>>Output: "`PAHNAPLSIIGYIR`"
>
>**Example 2:**
>
>>Input: s = "`PAYPALISHIRING`", numRows = 4  
>>Output: "`PINALSIGYAHRPI`"
>>Explanation:
>>
>>```java
>>P     I    N
>>A   L S  I G
>>Y A   H R
>>P     I
>>```

## 解法

如果按照最后输出的顺序遍历原字符串，那就变成了一个找规律的题目。

设`steps = (numRows - 1) * 2`：

- 第一行： `0, 0 + steps, 0 + 2 * steps, ...`
- 最后一行： `numRows - 1, (numRows - 1) + steps, (numRows - 1) + 2 * steps, ...`
- 中间第i行： `i, steps - i, steps + i, 2 * steps - i, ...`

用一个char[]存储所有字符，时间复杂度O(N)，空间O(N)。

```java
public String convert(String s, int numRows) {
        if (numRows < 2) return s;
        int steps = (numRows - 1) * 2, n = s.length(), count = 0;
        char[] zigzag = new char[n];
        for (int i = 0; i< numRows; i++)
            for (int j = 0; j + i < n; j+=steps){
                zigzag[count++] = s.charAt(i+j);
                if (i!= 0 && i!= numRows - 1 && j+ steps - i < n)
                    zigzag[count++] = s.charAt(j + steps - i);
            }
        return new String(zigzag);
    }
```
