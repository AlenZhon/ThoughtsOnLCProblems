# 217. Contains Duplicate

## 题目

>Given an array of integers, find if the array contains any duplicates.
>
>Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
>
>**Example 1:**
>
>>Input: [1,2,3,1]  
>>Output: true
>
>**Example 2:**
>
>>Input: [1,2,3,4]  
>>Output: false
>
>**Example 3:**
>
>>Input: [1,1,1,3,3,4,3,2,4,2]  
>>Output: true

## 解法

暴力遍历 + HashSet，5行代码完事。  
由于每一次查找和插入基本是常数时间，时间复杂度O(n)。空间复杂度O(n)。这个思路也是Solution中的Approach 3，但在*Note*中提示如果n不大的情况下，使用排序的时间复杂度小于HashSet。

### Note
>
>For certain test cases with not very large nnn, the runtime of this method can be slower than Approach #2. The reason is hash table has some overhead in maintaining its property. One should keep in mind that real world performance can be different from what the Big-O notation says. The Big-O notation only tells us that for sufficiently large input, one will be faster than the other. Therefore, when nnn is not sufficiently large, an O(n) algorithm can be slower than an O(nlog⁡n) algorithm.

使用排序算法（如堆排序）的时间复杂度为O(nlogn)，再进行遍历是O(n)。空间复杂度可为O(1)。

```java
public boolean containsDuplicate(int[] nums) {
        if (nums.length ==0 || nums.length ==1) return false;
        Arrays.sort(nums);
        for (int i =0; i<nums.length -1; i++)
            if (nums[i] == nums[i+1])
                return true;
        return false;
    }
```
