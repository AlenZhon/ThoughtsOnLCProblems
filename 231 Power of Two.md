# 231. Power of Two

## 题目

给定一个整数n，判断它是否是2的整数幂

>Given an integer, write a function to determine if it is a power of two.
>
>Example 1:
>
>>Input: 1  
>>Output: true  
>>Explanation: 2^0 = 1
>
>Example 2:
>
>>Input: 16  
>>Output: true  
>>Explanation: 2^4 = 16
>
>Example 3:
>
>>Input: 218  
>>Output: false

## 想法

计算n二进制里1的个数，如果大于1就return false  
和 *#191 Number of 1 Bits* 很像了。

```java
public boolean isPowerOfTwo(int n) {
        int count = 0;
        while (n >0) {
            count += (n & 0x1);
            n = n >>> 1;
            if (count>1) return false;
        }
        return (count == 1);
}
```

原来`Integer`类里就有这个方法`bitCount()`。时间复杂度为O(1)，。但是要注意 `0b1...0 = -2147483648`不是2的幂。

```java
return n > 0 && Integer.bitCount(n) == 1;
```

如果使用位运算，还有一个trick： `n & (n-1) == 0`

>If n is the power of two:
>
>>n = 2 ^ 0 = 1 = 0b0000...00000001, and (n - 1) = 0 = 0b0000...0000.  
>>n = 2 ^ 1 = 2 = 0b0000...00000010, and (n - 1) = 1 = 0b0000...0001.  
>>n = 2 ^ 2 = 4 = 0b0000...00000100, and (n - 1) = 3 = 0b0000...0011.  
>>n = 2 ^ 3 = 8 = 0b0000...00001000, and (n - 1) = 7 = 0b0000...0111.  
>
>we have n & (n-1) == 0b0000...0000 == 0
>
>Otherwise, n & (n-1) != 0.
>
>For example, n =14 = 0b0000...1110, and (n - 1) = 13 = 0b0000...1101.
>
>```java
>return n > 0 && ((n & (n-1)) == 0);
>```
>
>Time complexity = O(1)

此外，正整数范围内2的整数幂只有31个，直接查表也可以，时间复杂度O(1)。

```java
return new HashSet<>(Arrays.asList(1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576, 2097152, 4194304, 8388608,16777216, 33554432, 67108864, 134217728, 268435456, 536870912, 1073741824)).contains(n);
```
