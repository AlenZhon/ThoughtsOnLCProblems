# 443. String Compression

## Problems

将一个字符数组**in-place**压缩。要求空间复杂度为O(1)

>Given an array of characters, compress it **in-place**.
>
>The length after compression must always be smaller than or equal to the original array.
>
>Every element of the array should be a character (not int) of length 1.
>
>After you are done modifying the input array in-place, return the new length of the array.
>
>**Follow up:**
>Could you solve it using only O(1) extra space?
>
>**Example 1:**
>>
>>Input:  
>>["a","a","b","b","c","c","c"]
>>
>>Output:  
>>Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
>>
>>Explanation:
>>"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".

## 解法

一开始没有看懂题目，把compress当做是统计字符串中字符的出现频次，如果开HashMap或者哈希数组就不满足O(1)了。强行增加题目难度。

其实压缩题目的意思是连续出现的字符。比如`bbabb`压缩后变成`"b","2","a","b","2"`（"a"不用写1不然就达不到`The length after compression must always be smaller than or equal to the original array.`的要求了）。想到这里就可以采用2-pointer构造滑动窗口去做。

```java
 public int compress(char[] chars) {
        int slow =0, fast =0;
        for (int i =0; i< chars.length; i++) {
            if (i + 1 == chars.length || chars[i+1] != chars[i]) {
                chars[fast++] = chars[slow];
                if (i > slow) {
                   for (char c : ("" + (i - slow + 1)).toCharArray())
                       chars[fast++] = c;
                }
                slow = i +1;
            }
        }
        return fast;
    }
```

最里面那个for 是将次数转化为对应的字符。比如b出现了10次，就得变成"1","0"存进去。
