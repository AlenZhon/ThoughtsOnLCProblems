# 806. Number of Lines To Write String

## 题目

现在有一张特殊的信纸，信纸上每行有100格。给定了写26个小写字母的时候分别需要多少格的 `widths[]` 数组，以及要写的文本内容`String S` 。如果当前行所剩的格数不够写要写的字母，就得另起一行来写。返回总共需要写几行，以及最后一行占了多少格。

>We are to write the letters of a given string `S`, from left to right into lines. Each line has maximum width 100 units, and if writing a letter would cause the width of the line to exceed 100 units, it is written on the next line. We are given an array `widths`, an array where `widths[0]` is the width of 'a', widths[1] is the width of 'b', ..., and `widths[25]` is the width of 'z'.
>
>Now answer two questions: how many lines have at least one character from `S`, and what is the width used by the last such line? Return your answer as an integer list of length 2.
>
>**Example :**
>>Input:  
>>widths = `[10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10]`  
>>S = `"abcdefghijklmnopqrstuvwxyz"`  
>>Output: [3, 60]  
>>Explanation:  
>>All letters have the same length of 10. To write all 26 letters,  
>>we need two full lines and one line with 60 units.
>
>**Example :**
>>Input:  
>>widths = `[4,10,10,10,10,10,10,10,10,10,10,10,>>10,10,10,10,10,10,10,10,10,10,10,10,10,10]`  
>>S = `"bbbcccdddaaa"`  
>>Output: [2, 4]  
>>Explanation:  
>>All letters except 'a' have the same length of 10, and `"bbbcccdddaa"` will cover `9 * 10 + 2 * 4 = 98` units.  
>>For the last 'a', it is written on the second line because there is only 2 units left in the first line. So the answer is 2 lines, plus 4 units in the second line.
>
>Note:
>
> - The length of S will be in the range `[1, 1000]`.
> - `S` will only contain lowercase letters.
> - `widths` is an array of length 26.
> - `widths[i]` will be in the range of `[2, 10]`.

## 解法

没啥骚想法，直接写。时间复杂度和空间复杂度都和字符串S的长度线性相关。

```java
public int[] numberOfLines(int[] widths, String S) {
        int window = 0, lines = 0;
        for (char c : S.toCharArray()){
            if (window + widths[c - 'a'] > 100){
                lines++;
                window = widths[c - 'a'];
            } else
                window += widths[c- 'a'];
        }
        return new int[]{window != 0 ? lines + 1: lines, window};
    }
```
