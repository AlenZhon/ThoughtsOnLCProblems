# 693. Binary Number with Alternating Bits

## 题目

给定一个正整数，判断它的二进制形式中01是否交替出现。比如`5 = (101)_2， 10 = (1010)_2` 。

>Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.
>
>**Example 1:**
>
>>Input: 5  
>>Output: True  
>>Explanation:  The binary representation of 5 is: 101
>
>**Example 2:**
>
>>Input: 7  
>>Output: False  
>>Explanation:
>>The binary representation of 7 is: 111.
>
>**Example 3:**
>
>>Input: 11  
>>Output: False  
>>Explanation:
>>The binary representation of 11 is: 1011.
>
>**Example 4:**
>
>>Input: 10  
>>Output: True  
>>Explanation:
The binary representation of 10 is: 1010.

## 解法

除2取余，交替比较即可。`n /= 2`和`bit = n % 2`可代换成 `n >>= 1`和 `bit = n & 1`。

时间复杂度O(1)（Integer最多循环32次），空间O(1)。

```java
public boolean hasAlternatingBits(int n) {
        int bit = n % 2;
        for (int x = n / 2; x > 0; x /=2 ) {
            int curr = x & 1;
            if (curr == bit) return false;
            bit = curr;
        }
        return true;
    }
```

### Alternative

可以用Integer的类方法 `Integer.toBinaryString(int i)` 转化成二进制字符串然后再逐个比较字符。 时间和空间复杂度也为O(1)。
