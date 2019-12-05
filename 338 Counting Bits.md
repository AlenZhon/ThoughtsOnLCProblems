# 338. Counting Bits

## 题目

给定一个非负整数num，求[0, num]范围内所有整数的二进制表示形式各有多少个1，用数组形式存储并返回。

>Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.
>
>**Example 1:**
>
>>Input: 2  
>>Output: [0,1,1]  
>
>**Example 2:**
>
>>Input: 5  
>>Output: [0,1,1,2,1,2]
>
>Follow up:
>
> - It is very easy to come up with a solution with run time **O(n*sizeof(integer))**. But can you do it in linear time **O(n)** /possibly in a single pass?
> - Space complexity should be `O(n)`.
> - Can you do it like a boss? Do it without using any builtin function like **__builtin_popcount** in c++ or in any other language.

## 解法

follow-up里说的**O(n*sizeof(integer))**算法即为暴力破解方法。 (2ms)

```java
public int[] countBits(int num) {
        int[] ret = new int[num + 1];
        for (int i =0; i<= num; i++) {
            int count = 0, x = i;
            while (x > 0) {
                count += (x & 1);
                x>>= 1;
            }
            ret[i] = count;
        }
        return ret;
    }
```

如果要达到One-pass O(n)的时间复杂度，就得找找规律。

写出数组的前几项看看。

```java
0,
1,
1,2,
1,2,2,3,
1,2,2,3,2,3,3,4,
1,2,2,3,2,3,3,4,2,3,3,4,3,4,4,5
...
```

在这里为了找规律写成了多行的形式。可以看出给定初始值0,1，后面所有的数字都是由前一行变化而来。一行写满时，当前一行的元素个数总是前一行的两倍，设前一行的个数为n，则当前行的前n个元素和前一行的n个元素相同，后n个元素是前一行n个元素的依次增1.

通过这个规律写了一版。( 还是2ms? 这个不算O(n)吗? )

```java
public int[] countBits(int num) {
        if (num == 0) return new int[]{0};
        else if (num == 1) return new int[]{0, 1};
        int[] ret = new int[num + 1];
        int prev = 1, curr = 0;
        for (int i = 0; i <= num; i++){
            if (i < (prev + prev / 2)) ret[i] = ret[++curr];
            else if (i < prev * 2) ret[i] = ret[++curr] + 1;
            else {
                curr = prev;
                prev = i;
                ret[i] = 1;
            }
        }
        return ret;
    }
```

如果我们回看暴力破解的方法，就会发现每次算1的个数包含了大量的重复计算。实际上不需要把x的每一位拆开，只需判断x的最后一位是0还是1，然后其他位置上的1的个数已经由 (x>>1)算过了。 (1ms)

```java
public int[] countBits(int num) {
        int[] ret = new int[num + 1];
        for (int i = 1; i<= num; i++) {
            ret[i] = ret[i >> 1] + (i & 1);
        }
        return ret;
    }
```
