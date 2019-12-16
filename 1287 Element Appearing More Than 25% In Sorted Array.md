# 1287. Element Appearing More Than 25% In Sorted Array

## 题目

数组中有且只有一个元素出现频次大于25%。找到这个元素。
>Given an integer array sorted in non-decreasing order, there is exactly one integer in the array that occurs more than 25% of the time.
>
>Return that integer.
>
>**Example 1:**
>
>>Input: arr = [1,2,2,6,6,6,6,7,10]  
>>Output: 6
>
>**Constraints:**
>
> - 1 <= arr.length <= 10^4
> - 0 <= arr[i] <= 10^5

## 解法

无脑遍历。时间复杂度O(n)。

```java
public int findSpecialInteger(int[] arr) {
        int freq = arr.length / 4, prev = arr[0], nowFreq = 1;
        for (int i = 1; i< arr.length; i++){
            if (arr[i] == prev) nowFreq++;
            else {
                prev = arr[i];
                nowFreq = 1;
            }
            if (nowFreq > freq) return prev;
        }
        return arr[0];
    }
```
