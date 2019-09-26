# 485. Max Consecutive Ones

## 题目

一个二值化的int[] 数组，求出其中连续出现1的最大长度。

>Given a binary array, find the maximum number of consecutive 1s in this array.
>
>**Example 1:**
>
>>Input: [1,1,0,1,1,1]  
>>Output: 3  
>>Explanation: The first two digits or the last three digits are consecutive 1s.  The maximum number of consecutive 1s is 3.
>
>**Note:**
>
> - The input array will only contain 0 and 1.
> - The length of input array is a positive integer and will not exceed 10,000.

## 解法

水题。用`currmax`和`max`当前连续1的长度和移遍历的最大长度，遍历时每次碰到0，清空currmax，更新max。最后再更新一次max即可。

```java
public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0, currmax = 0;
        for (int n : nums) {
            currmax += n;
            if (n == 0) {
                max = (currmax > max) ? currmax : max;
                currmax = 0;
            }
        }
        return currmax > max ? currmax : max;
    }
```
