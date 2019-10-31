# 704. Binary Search

## 题目

给定一个元素互不相同的有序数组 nums 和一个数 target。判断 target 是否在数组中，返回所在下标；如果不在则返回-1.

>Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.
>
>Example 1:
>
>>Input: nums = `[-1,0,3,5,9,12]`, target = 9  
>>Output: 4  
>>Explanation: 9 exists in nums and its index is 4
>
>Example 2:
>
>>Input: nums = `[-1,0,3,5,9,12]`, target = 2  
>>Output: -1
>>Explanation: 2 does not exist in nums so return -1
>
>**Note:**
>
> - You may assume that all elements in nums are unique.
> - n will be in the range `[1, 10000]`.
> - The value of each element in nums will be in the range `[-9999, 9999]`.

## 解法

题目都写明白了，二分查找。注意边界条件的判断（是否取等/下标怎么更新）。

```java
public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            if (nums[left] == target) return left;
            if (nums[right] == target) return right;
            int mid = left + (right - left) /2;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return -1;
    }
```

时间复杂度 O(logn), 空间 O(1)
