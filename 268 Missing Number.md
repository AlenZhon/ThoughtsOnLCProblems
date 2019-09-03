# 268. Missing Number

## 题目

给定只差一个整数的非负整数数列，找出差的那个整数。

>Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.
>
>**Example 1:**
>
>>Input: [3,0,1]  
>>Output: 2
>
>**Example 2:**
>
>>Input: [9,6,4,2,3,5,7,0,1]  
>>Output: 8
>
>**Note:**
>Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## 解法

看到note首先排除时间空间都为O(n)的暴力破解hashset方法。  
（Solution里还列举了一种方法用排序找missing number，时间复杂度排序的O(nlogn)+遍历的O(n)，空间复杂度O(1)或O(n)）

容易发现missing number = (数列元素之和)-(数列下标之和)。（也是Solution Approach 4的写法）。为了防止两个和数值溢出，可以在遍历时只增加每个元素与其下标的差值。

```java
public int missingNumber(int[] nums) {
        int ret = 0;
        for (int i = 0; i<nums.length; i++)
            ret = ret + i + 1 - nums[i];
        return ret;
    }
```

Approach 3用的是异或运算，初始值为数组长度，数组元素异或下标两两相等则抵消，运算结果就是落单的missing number。

```java
 public int missingNumber(int[] nums) {
        int ret = nums.length;
        for (int i = 0; i<nums.length; i++)
            ret ^= i^nums[i];
        return ret;
    }
```

## Notes

在 *#136 Single number*中也出现了异或运算。
