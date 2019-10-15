# 38. Count and Say

## 题目

从字符串"1"开始作为第一次输入，将输入念一遍作为输入（如"1个1"即"11"）。  
下一次的输入即为此次输出，则第二次输入为"11"，输出为"2个1"即"21"。  
现在给定次数n(`1<= n<= 30`)，求第n次的输出字符串。

>The **count-and-say** sequence is the sequence of integers with the first five terms as following:
>
>>1. 1
>>2. 11
>>3. 21
>>4. 1211
>>5. 111221
>
>1 is read off as "one 1" or 11.  
>11 is read off as "two 1s" or 21.  
>21 is read off as "one 2, then one 1" or 1211.  
>
>Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence.
>
>Note: Each term of the sequence of integers will be represented as a string.
>
>Example 1:
>
>>Input: 1  
>>Output: "1"  
>
>Example 2:
>
>>Input: 4  
>>Output: "1211"

## 解法

按照题目意思翻译了一下。用`StringBuilder`作为每次存放新字符串的存储空间。

```java
 public String countAndSay(int n) {
        if (n == 1) return "1";
        StringBuilder sb = new StringBuilder();
        String s = "11";
        for (int i = 2; i < n; i++) {
            sb.setLength(0);
            int count = 0, top = 0, curr = 0;
            for (; curr < s.length(); curr++) {
                if (s.charAt(top) == s.charAt(curr))
                    count++;
                else {
                    sb.append(count).append(s.charAt(top));
                    count = 1; //设1 表示新的top已经出现了1次
                    top = curr;
                }
            }
            sb.append(count).append(s.charAt(curr - 1));
            s = sb.toString();
        }
        return s;
    }
```

提交运行时间2ms，看了一眼0ms的解法，是把1到30的结果全部存在`String[]`，暴力查表。牛逼
