# 868. Binary Gap

## 题目

一个十进制自然数，找到它二进制形式下相邻两个1间隔最远的距离。如22 = (10110)_2，总共三个1，前面两个1相距最远，为2，所以返回2。

>Given a positive integer N, find and return the longest distance between two consecutive 1's in the binary representation of N.
>
>If there aren't two consecutive 1's, return 0.
>
>**Example 1:**
>
>>Input: 22  
>>Output: 2  
>>Explanation:  
>>22 in binary is 0b10110.  
>>In the binary representation of 22, there are three ones, and two consecutive pairs of 1's.  
>>The first consecutive pair of 1's have distance 2.  
>>The second consecutive pair of 1's have distance 1.  
>>The answer is the largest of these two distances, which is 2.  
>
>**Example 2:**
>
>>Input: 5  
>>Output: 2  
>>Explanation:  
>>5 in binary is 0b101.
>
>**Example 3:**
>
>>Input: 6  
>>Output: 1  
>>Explanation:  
>>6 in binary is 0b110.  
>
>**Example 4:**
>
>>Input: 8  
>>Output: 0  
>>Explanation:  
>>8 in binary is 0b1000.  
>>There aren't any consecutive pairs of 1's in the binary representation of 8, so we return 0.
>
>**Note:**
>
> - 1 <= N <= 10^9

## 解法

水题。时间复杂度O(log_2 N)，空间O(1)。

```java
public int binaryGap(int N) {
        int gap = 0, prev = -1, count = -1;
        for (int i = 0; i< 32; i++){
            count++;
            if (((N >> i) & 1) == 1) {
                if (prev > -1) gap = count - prev > gap ? count - prev : gap;
                prev = count;
            }
        }
        return gap;
    }
```

不过一开始报错：

>`bad operand types for binary operator ＂&＂`

仔细看了一下，发现是运算优先级的问题。原来没有加括号`(N >> i) & 1 == 1`，而 **`==` 的优先级比位运算符要高**，所以变成了`(N >> i) & (1 == 1)`。
